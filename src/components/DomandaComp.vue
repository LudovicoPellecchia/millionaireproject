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
    <div class="domanda-style">
        <div>
            {{ quiz?.domanda }}
        </div>
    </div>
</template>

<style lang="scss" scoped>
.domanda-style {
    text-align: center;
    margin-bottom: 80px;

    div {
        border-radius: 40px;
        padding: 20px 40px;
        background-color: wheat;
        display: inline-block;
    }
}
</style>