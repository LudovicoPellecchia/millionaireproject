<script>

export default {

    props: {
        quiz: Object
    },

    data() {
        return {
        }
    }
}
</script>


<template>
    <div v-if="quiz" class="domanda-style">
        <div>
            {{ quiz?.domanda }}
        </div>
    </div>
</template>

<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Anonymous+Pro);

.domanda-style {
    text-align: center;
    margin-bottom: 80px;

    div {
        font-family: 'Anonymous Pro', monospace;
        color: white;
        border-radius: 40px;
        padding: 20px 40px;
        background-color: #A01A7D;
        display: inline-block;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);;
    }
}
</style>