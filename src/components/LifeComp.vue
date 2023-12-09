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
        <i :class="{
            'pulse-animation': errorCounter >= 2,
            'fa-regular fa-heart underline': errorCounter >= 3,
            'fa-solid fa-heart': errorCounter < 3
        }"></i>
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

.pulse-animation {
    transform: scale(1);
    animation: pulse 1.5s 3;
}

@keyframes pulse {
    0% {
        transform: scale(1);
    }

    40% {
        transform: scale(0.90);
    }

    100% {
        transform: scale(1);
    }
}
</style>