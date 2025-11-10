<template>
    <main class="AlexiconMasonry-MAIN">
        <div class="AlexiconMasonry-col" :style="`width: ${ 100 / colsNum }%;`" v-for="(item, index) in finalArray" :key="index">
            <div v-for="(subItem, subIndex) in item" :key="subIndex">

                <img :src="subItem.url || subItem" v-if="mediaIsFormat('img', subItem)">

                <video v-if="mediaIsFormat('video', subItem)">
                    <source :src="subItem.url || subItem" :type="subItem.type">
                    Your browser does not support the video tag.
                </video>

            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'AlexiconMasonry',
    props: {
        media: Array,
        colsNum: Number,
    },
    data(){
        return{
            finalArray: [],
        }
    },
    methods: {
        generateArrayColumns(){
            const media = this.media;
            const n = this.colsNum;

            for(let i = 0; i < n; i++)
                this.finalArray.push([]);

            let selector = 0;
            for(let i of media){
                this.finalArray[selector].push(i)
                selector = selector < n - 1 ? selector + 1 : 0;
            }
        },

        mediaIsFormat(type, url){
            const format = url.type?.split('/')[1] || url.split('.')[url.split('.').length-1];
            let arr = [];

            if(type == 'img') arr =['jpg', 'jpeg', 'png', 'gif', 'webp'];
            if(type == 'video') arr = ['mp4', 'mov', 'webm'];

            return arr.includes(format);
        }
    },
    mounted(){
        this.generateArrayColumns();
    }
}
</script>

<style scoped lang="stylus">
.AlexiconMasonry-MAIN
    width: 100%
    display: flex

.AlexiconMasonry-col
    display: flex
    flex-direction: column
    align-items: center

    >div
        width: 100%
        display: block

        >img
        >video
            display: block
            width: 100%
            border-radius: 5px
            scale: 0.97
            margin: 0

            &:hover
                cursor: pointer
                filter: brightness(0.8)
                transition: filter 0.2s
</style>