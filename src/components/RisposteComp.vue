<script>

export default {

    props: {
        quiz: Object
    },

    data() {
        return {
            isCorrect: false
        }
    },

    methods: {
        selectOption(option) {
            if(option === this.quiz.rispostaCorretta){
                this.isCorrect = true
            }
            this.$emit('optionSelected', option, this.isCorrect);
        },

    }
}
</script>


<template>
    <div class="container my-style-container">
        <div class="row row-cols-2 gy-3">
            <div class="col d-flex justify-content-center" v-for="opzione in quiz?.opzioni" :key="opzione">
                <div class="items" @click="selectOption(opzione)"
                    :class="isCorrect ? 'correct-answer' : ''">
                    {{ opzione }}
                </div>
            </div>

        </div>

    </div>
</template>

<style lang="scss" scoped>
.items {
    background-color: #E09F7D;
    width: 70%;
    font-weight: 600;
    border: 1px solid #311847;
    text-align: center;
    margin-top: 14px;
    list-style: none;
    cursor: pointer;
    padding: 10px 14px;
    box-shadow: 10px 10px #311847;
    transition: transform 500ms, box-shadow 500ms;

    &:hover {
        transform: scale(1.1);
        box-shadow: 10px 10px 2px #311847;
    }

}

.correct-answer {
    background-color: #B1CC74 !important;
}
</style>