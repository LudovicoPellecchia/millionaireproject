<script>

export default {

    props: {
        progress: Number
    },

    data() {
        return {
        }
    }
}
</script>


<template>
    <div class="my-progress-bar-container">
        <div class="my-progress-bar" :style="{ width: `${progress * 100}%` }"></div>
    </div>
</template>

<style lang="scss" scoped>
.my-progress-bar-container {
    background-color: rgba(255, 255, 255, 0.334);
    border-radius: 50px;
    margin-bottom: 40px;
    width: 100%;
    height: 10px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);;


    .my-progress-bar {
        height: 100%;
        background-color: #B1CC74;
        transition: width 0.5s ease; /* Aggiungi una transizione fluida */


    }
}
</style>