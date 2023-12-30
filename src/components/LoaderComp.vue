<script>

export default {

    data() {
        return {
        }
    }
}
</script>


<template>
    <div class="loader">
<!--         <div class="loading-text">
            Stiamo generando il tuo quiz
        </div> -->
        <div class="dot-flashing"></div>
    </div>
</template>

<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Anonymous+Pro);

.loading-text {
    font-family: 'Anonymous Pro', monospace;
}

.loader{
    transition: opacity 2s;
    opacity: 1;
    align-items: center;
    display: flex;
    flex-direction: column;
    gap: 10px;
    justify-content: center;
}

.dot-flashing {
    position: relative;
    width: 40px;
    height: 40px;
    border-radius: 10px;
    background-color: rgb(0, 19, 33);
    color: #9880ff;
    animation: dot-flashing 1s infinite linear alternate;
    animation-delay: 0.5s;
}

.dot-flashing::before,
.dot-flashing::after {
    content: "";
    display: inline-block;
    position: absolute;
    top: 0;
}

.dot-flashing::before {
    left: -55px;
    width: 40px;
    height: 40px;
    border-radius: 10px;
    background-color: rgb(0, 19, 33);
    color: #9880ff;
    animation: dot-flashing 1s infinite alternate;
    animation-delay: 0s;
}

.dot-flashing::after {
    left: 55px;
    width: 40px;
    height: 40px;
    border-radius: 10px;
    background-color: rgb(0, 19, 33);
    color: #9880ff;
    animation: dot-flashing 1s infinite alternate;
    animation-delay: 1s;
}

@keyframes dot-flashing {
    0% {
        background-color:rgb(0, 19, 33);
    }

    50%,
    100% {
        background-color: rgba(0, 19, 33, 0.2);
    }
}
</style>