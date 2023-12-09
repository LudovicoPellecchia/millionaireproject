<script>


export default {
    components: {
    },

    props: {
    },

    data() {
        return {
        }
    }
}
</script>


<template>
    <div class="transform ">

        <h1 class="title typewriter">
            <div class="hidden-text">
                <span class="apici">&ldquo;</span>
                DO
            </div>
            <div class="hidden-text">YOUR</div>
            <div class="hidden-text">QUIZ!</div>
        </h1>
    </div>
</template>

<style lang="scss" scoped>
.apici {
    display: block;
    position: absolute;
    top: -25px;
    left: -25px;
}

.transform {
    display: flex;
    justify-content: center;
    padding-top: 30px;
    transform: skewY(-4deg);
}

/* .hidden-text {
    opacity: 0;
}
 */
div:nth-child(1) {
    position: relative;
    animation:
        show-text forwards
}

div:nth-child(2) {
    text-align: center;
    animation:
        show-text 0s 1.5s forwards
}

div:nth-child(3) {
    text-align: end;
    animation:
        show-text 0s 2.5s forwards
}

.title {
    background-size: cover;
    width: 50%;

    align-items: center;
    margin-top: 20px;
    letter-spacing: 10px;
    font-size: 4.2rem;
    text-shadow: 3px 7px rgb(196, 35, 102);
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    color: white;
    /*     padding: 20px 40px;
 */
    /*   box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
 */

}


.typewriter h1 div {

    overflow: hidden;
    /* Ensures the content is not revealed until the animation */
    border-right: .07em solid white;
    /* The typwriter cursor */

    /* Gives that scrolling effect as the typing happens */
    letter-spacing: .07em;
    /* Adjust as needed */


}

@keyframes show-text {
    from {
        opacity: 0;
    }

    to {
        opacity: 1;
    }
}
</style>