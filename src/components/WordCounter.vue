<template>
<div class="body">
    <div>
        <textarea class="text-box" v-model="text" placeholder="Add text to be counted..."></textarea>
    </div>
    <ul class="analytics">
        <li class="text-data">Character Count: {{characterCount}}</li>
        <li class="text-data">Word Count: {{wordCount}}</li>
        <li class="text-data">Paragraph Count: {{paraCount}}</li>
        <li class="text-data">Sentences Count: {{sentenceCount-1}}</li>
        <li class="text-data">Time to Read: {{readTime}}</li>
    </ul>
</div>
</template>

<script>
export default {
    name: "WordCounter",
    data() {
        return {
            text: "",
        }
    },
    methods: {
        countWords() {
            let handleWords = this.text.replace(/(^\s*)|(\s*$)/gi, "");
            handleWords = handleWords.replace(/[ ]{2,}/gi, " ");
            handleWords = handleWords.replace(/\n /, "\n");
            let finalCount = handleWords.split(' ').length;
            return finalCount;
        }
    },
    computed: {
        wordCount() {
            return this.countWords();
        },
        paraCount() {
            let paraLength = this.text.replace(/\n$/gm, '').split(/\n/).length;
            return paraLength;
        },
        characterCount() {
            let charaCount = this.text.split('');
            return charaCount.length;
        },
        sentenceCount() {
            let sentCount = this.text.split(/[.|!|?]+/g).length;
            return sentCount;
        },
        readTime() {
            const wordsPerMinute = 200;
            let result;
            let wordCounter = this.countWords();
            if (wordCounter > 0) {
                let time = Math.ceil(wordCounter / wordsPerMinute);
                result = `~${time} min read`;
            }
            return result;
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
.body {

    .text-box {
        width: 60%;
        height: 40vh;
    }

    .analytics {
        display: flex;
        justify-content: center;

        .text-data {
            padding: 3%;
            list-style: none;
        }

    }

}
</style>
