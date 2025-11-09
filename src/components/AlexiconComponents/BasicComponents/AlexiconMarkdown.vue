<template>
    <div class="AlexiconMarkdown-MAIN" v-html="result"></div>
    <div class="AlexiconMarkdown-spoiler"><label><input type="checkbox"/><div>spoiler text</div></label></div>
</template>

<script>
import { Marked } from 'marked';
import markedKatex from "marked-katex-extension";
import { markedHighlight } from "marked-highlight";
import hljs from 'highlight.js';
import 'highlight.js/styles/tokyo-night-dark.css';

export default {
    name: 'AlexiconMarkdown',
    props:{
        styles: Object,
        val: undefined,
    },
    data(){
        return{
            result: '',
        }
    },
    methods: {
        renderMarkdown(){
            const options = {
                throwOnError: false,
            };

            const marked = new Marked(
                markedHighlight({
                    emptyLangClass: 'hljs',
                    langPrefix: 'hljs language-',
                    // eslint-disable-next-line no-unused-vars
                    highlight(code, lang, info) {
                        const language = hljs.getLanguage(lang) ? lang : 'plaintext';
                        return hljs.highlight(code, { language }).value;
                    },
                })
            );
            marked.use(markedKatex(options));

            const html = marked.parse(this.val);
            this.result = this.postProcessing(html);
        },

        postProcessing(text){
            let result = text.replaceAll(
                /<blockquote>\s*<p>!(.*?)<\/p>\s*<\/blockquote>/gs,
                '<div class="AlexiconMarkdown-spoiler"><label><input type="checkbox"/><div>$1</div></label></div>'
            );

            return result;
        }
    },
    mounted(){
        this.renderMarkdown();
    }
}
</script>

<style scoped lang="stylus">
.AlexiconMarkdown-MAIN
    font-size: 1.5ch

    :deep(th)
        border: 1px solid rgba(128, 128, 128, 0.2)

    :deep(td)
    :deep(th)
        padding: 0 1ch

    :deep(tbody) > tr:nth-child(odd)
        background-color: rgba(128, 128, 128, 0.2)

    :deep(blockquote)
        border-left: 6px solid rgba(128, 128, 128, 0.2)
        padding-left: 1ch

    :deep(pre) > code
        padding: 1ch
        background-color: rgb(26, 27, 38)
        color: rgb(154, 165, 206)
        font-family: "Roboto Mono", serif

/* post processing */

    :deep(.AlexiconMarkdown-spoiler)

        label
            position relative;

        div
            padding: 5px 10px;
            background-size: 3px 3px /* Adjusts the spacing of the dots */
            width: fit-content

        input
            position absolute
            opacity 0

            &:not(:checked) ~ div
                cursor: help
                color: transparent
                background-image: radial-gradient(rgba(128, 128, 128, 0.5) 1px, transparent 1px) /* Creates the dots */

            &:checked ~ div
                background-image: radial-gradient(rgba(128, 128, 128, 0.25) 1px, transparent 1px);/* Creates the dots */      
</style>