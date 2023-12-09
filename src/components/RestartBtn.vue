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
    color: white;
    cursor: pointer;
    margin-top: 50px;
    display: inline-block;
    padding: 15px 20px;
    border: 1px solid rgb(189, 49, 170);
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);;

    border-radius: 50px;
    transition: background-color 500ms;

    &:hover {
        background-color: #A01A7D;

        animation: tilt-shaking 0.2s infinite 0.4s ease-in-out;

@keyframes tilt-shaking {
    0% {
        transform: rotate(0deg);
    }

    25% {
        transform: rotate(0.5deg);
    }

    50% {
        transform:rotate(0eg);
    }

    75% {
        transform: rotate(-0.5deg);
    }

    100% {
        transform: rotate(0deg);
    }
}
    }
}
</style>