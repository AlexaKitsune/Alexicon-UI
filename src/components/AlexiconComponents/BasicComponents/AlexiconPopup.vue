<template>
    <div class="AlexiconPopup-MAIN">
        <X @click="close()" class="AlexiconPopup-close"/>
        <p><b>{{ title }}</b></p>
        <p>{{ text }}</p>
    </div>
</template>

<script>
import { X } from 'lucide-vue-next';
export default {
    name: 'AlexiconPopup',
    components: {
        X
    },
    props: {
        title: String,
        text: String,
    },
    methods: {
        close(){
            this.$emit('close', true);
        }
    }
}
</script>

<style lang="stylus">
.AlexiconPopup-MAIN
    z-index: 2;
    max-width: calc(100% - 40px);
    width: fit-content;
    min-width: 25px;
    min-height: 25px;
    position: fixed;
    left: 0;
    right: 0;
    margin: 0 auto;
    margin-top: 10px;
    background-color: #F8F3D6;
    color: #916C2A;
    border-radius: 5px;
    border: 2px solid #916C2A;
    padding: 5px 0;
    padding-right: 15px;

    p
        margin: 0 10px;

.AlexiconPopup-close
    position: absolute;
    top: 5px;
    right: 5px;
    color: #916C2A;
    width: 15px;
    height: 15px;

    &:hover
        scale: 1.1;
        cursor: pointer;
</style>