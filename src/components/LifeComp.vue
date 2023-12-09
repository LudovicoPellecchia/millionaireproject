<script>

export default {

    props: {
        errorCounter: Number
    },

    data() {
        return {
        }
    }
}
</script>


<template>
    <div class="life-container">
        <i :class="(errorCounter >= 3) ? 'fa-regular fa-heart underline' : 'fa-solid fa-heart'"></i>
        <i :class="(errorCounter >= 2) ? 'fa-regular fa-heart underline' : 'fa-solid fa-heart'"></i>
        <i :class="(errorCounter >= 1) ? 'fa-regular fa-heart underline' : 'fa-solid fa-heart'"></i>
    </div>
</template>

<style lang="scss" scoped>
.life-container {
    display: flex;
    gap: 10px;
}

.life-container i {
    color: rgb(194, 35, 101);
    font-size: 1.5rem;
    display: block;

}

.underline {
    text-decoration-line: line-through;
}
</style>