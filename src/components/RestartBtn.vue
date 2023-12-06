<script>

export default {

    props: {
    },

    data() {
        return {
        }
    }
}
</script>


<template>

    <div class="text-end">
        <div class="restart-btn">
            Ricomincia il gioco
        </div>
    </div>

</template>

<style lang="scss" scoped>
.restart-btn {
    cursor: pointer;
    margin-top: 50px;
    display: inline-block;
    padding: 12px 18px;
    border: 1px solid black;
    border-radius: 50px;
    transition: background-color 500ms;

    &:hover {
        background-color: wheat;
    }
}
</style>