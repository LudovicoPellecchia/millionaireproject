<script>

export default {

    props: {
        quiz: Object
    },

    data() {
        return {
        }
    },

    methods: {
        selectOption(option) {
            this.$emit('optionSelected', option);
        }
    }
}
</script>


<template>
    <div class="container">
        <div class="row row-cols-2">
            <div class="col" v-for="opzione in quiz?.opzioni" :key="opzione">
                
                    <div class="items" @click="selectOption(opzione)">{{ opzione }}</div>
                
            </div>

        </div>

    </div>
</template>

<style lang="scss" scoped>
.items {
    border: 1px solid black;
    text-align: center;
    margin-top: 14px;
    list-style: none;
    cursor: pointer;
    padding: 10px 14px;
}
</style>