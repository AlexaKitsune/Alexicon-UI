<template>
    <div class="mv-wrap" ref="wrap">
        <canvas ref="canvas"></canvas>
        <button class="mv-reset" @click="resetCamera">Reset cámara</button>
    </div>
</template>

<script>
import * as THREE from 'three'
import { markRaw } from 'vue'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import { GLTFLoader }  from 'three/examples/jsm/loaders/GLTFLoader.js'
import { DRACOLoader } from 'three/examples/jsm/loaders/DRACOLoader.js'
import { FBXLoader }   from 'three/examples/jsm/loaders/FBXLoader.js'
import { OBJLoader }   from 'three/examples/jsm/loaders/OBJLoader.js'
import { STLLoader }   from 'three/examples/jsm/loaders/STLLoader.js'

export default {
    name: 'ModelViewer',
    props: {
        modelUrl: { type: String, required: true },
        background: { type: String, default: '#0b1020' },
        grid: { type: Boolean, default: false }
    },
    data(){
        return {
        renderer: null,
        scene: null,
        camera: null,
        controls: null,
        rafId: null,
        currentModel: null
        }
    },
    methods: {
        addLights(){
            const hemi = markRaw(new THREE.HemisphereLight(0xffffff, 0x202020, 1.2))
            this.scene.add(hemi)
            const dir = markRaw(new THREE.DirectionalLight(0xffffff, 1.0))
            dir.position.set(5,5,5)
            this.scene.add(dir)
        },

        addGrid(){
            if(!this.grid) return
            const grid = markRaw(new THREE.GridHelper(20, 20, 0x44506b, 0x1f2937))
            // En algunas versiones GridHelper usa material array:
            const mats = Array.isArray(grid.material) ? grid.material : [grid.material]
            mats.forEach(m => { m.transparent = true; m.opacity = 0.25 })
            this.scene.add(grid)
        },

        fitToObject(object3D, padding = 1.2){
            const box = new THREE.Box3().setFromObject(object3D)
            if (box.isEmpty()) return
            const size = new THREE.Vector3()
            const center = new THREE.Vector3()
            box.getSize(size)
            box.getCenter(center)
            const radius = Math.max(size.x, size.y, size.z) * 0.5
            const fov = THREE.MathUtils.degToRad(this.camera.fov)
            const dist = (radius * padding) / Math.sin(fov / 2)
            const dir = new THREE.Vector3(1, 0.6, 1).normalize()
            this.camera.position.copy(center.clone().add(dir.multiplyScalar(dist)))
            this.camera.near = Math.max(0.01, dist / 100)
            this.camera.far = dist * 10
            this.camera.updateProjectionMatrix()
            this.controls.target.copy(center)
            this.controls.update()
        },

        getExt(url){
            const base = url.split('#')[0].split('?')[0]
            const i = base.lastIndexOf('.')
            return i >= 0 ? base.slice(i+1).toLowerCase() : ''
        },
        async disposeCurrent(){
            if (!this.currentModel) return
            this.scene.remove(this.currentModel)
            this.currentModel.traverse?.(n => {
                if (n.isMesh) {
                    n.geometry?.dispose?.()
                    if (Array.isArray(n.material)) n.material.forEach(m => m?.dispose?.())
                    else n.material?.dispose?.()
                }
            })
            this.currentModel = null
        },

        async loadModel(url){
            await this.disposeCurrent()
            const ext = this.getExt(url)
            let object

            if (ext === 'glb' || ext === 'gltf' || ext === 'vrm') {
                const loader = new GLTFLoader()
                const draco = new DRACOLoader()
                // DRACO por CDN. Si prefieres local: draco.setDecoderPath('/draco/')
                draco.setDecoderPath('https://unpkg.com/three@0.160.0/examples/jsm/libs/draco/')
                loader.setDRACOLoader(draco)
                object = await new Promise((resolve, reject) =>
                    loader.load(url, gltf => resolve(gltf.scene || gltf.scenes?.[0]), undefined, reject)
                )
            } else if (ext === 'fbx') {
                const loader = new FBXLoader()
                object = await new Promise((resolve, reject) =>
                    loader.load(url, resolve, undefined, reject)
                )
            } else if (ext === 'obj') {
                const loader = new OBJLoader()
                object = await new Promise((resolve, reject) =>
                    loader.load(url, resolve, undefined, reject)
                )
            } else if (ext === 'stl') {
                const loader = new STLLoader()
                const geom = await new Promise((resolve, reject) =>
                    loader.load(url, resolve, undefined, reject)
                )
                const mat  = markRaw(new THREE.MeshPhysicalMaterial({ color: 0x99aabb, metalness: 0.1, roughness: 0.5 }))
                object = markRaw(new THREE.Mesh(geom, mat))
            } else {
                throw new Error(`Extensión no soportada: ${ext}`)
            }

            // Asegura objetos "raw" antes de meterlos a la reactividad
            object = markRaw(object)
            object.name = '__MODEL__'
            this.scene.add(object)
            this.currentModel = object
            this.fitToObject(object)
        },

        initThree(){
            const canvas = this.$refs.canvas
            this.renderer = markRaw(new THREE.WebGLRenderer({ canvas, antialias: true }))
            this.renderer.outputColorSpace = THREE.SRGBColorSpace
            this.renderer.toneMapping = THREE.ACESFilmicToneMapping
            this.renderer.toneMappingExposure = 1.0

            this.scene = markRaw(new THREE.Scene())
            this.scene.background = new THREE.Color(this.background)

            this.camera = markRaw(new THREE.PerspectiveCamera(60, 1, 0.01, 1000))
            this.camera.position.set(2.5, 1.5, 3.5)

            this.controls = markRaw(new OrbitControls(this.camera, this.renderer.domElement))
            this.controls.enableDamping = true
            this.controls.target.set(0, 0.8, 0)

            this.addLights()
            this.addGrid()
            this.resizeRenderer()

            const animate = () => {
                this.controls.update()
                this.renderer.render(this.scene, this.camera)
                this.rafId = requestAnimationFrame(animate)
            }
            animate()

            window.addEventListener('resize', this.resizeRenderer, { passive: true })
        },
        
        resizeRenderer(){
            const w = this.$refs.wrap?.clientWidth || window.innerWidth
            const h = this.$refs.wrap?.clientHeight || window.innerHeight
            this.renderer.setSize(w, h, false)
            this.camera.aspect = w / h
            this.camera.updateProjectionMatrix()
        },

        async resetCamera(){
            if (this.currentModel) this.fitToObject(this.currentModel)
            else {
                this.camera.position.set(2.5, 1.5, 3.5)
                this.controls.target.set(0, 0.8, 0)
                this.controls.update()
            }
        }
    },
    async mounted(){
        this.initThree()
        if (this.modelUrl) {
            try { await this.loadModel(this.modelUrl) }
            catch (e) { console.error('Error cargando modelo:', e) }
        }
    },
    async beforeUnmount(){
        cancelAnimationFrame(this.rafId)
        window.removeEventListener('resize', this.resizeRenderer)
        this.controls?.dispose?.()
        this.renderer?.dispose?.()
        await this.disposeCurrent()
    },
    watch: {
        modelUrl: {
        immediate: false,
            handler: async function (url){
                if (!url) return
                try { await this.loadModel(url) }
                catch (e) { console.error('Error re-cargando modelo:', e) }
            }
        }
    }
}
</script>

<style scoped>
    .mv-wrap{
        position: relative;
        width: 100%;
        height: 100%;
        background: #0b1020;
    }

    canvas{ display:block; width:100%; height:100% }

    .mv-reset{
        position: absolute; right: 1rem; bottom: 1rem;
        background: rgba(255,255,255,.08);
        color: #cfd6e4; border: 1px solid rgba(255,255,255,.12);
        padding: .45rem .7rem; border-radius: .6rem; cursor: pointer;
    }

    .mv-reset:hover{ background: rgba(255,255,255,.14) }
</style>
