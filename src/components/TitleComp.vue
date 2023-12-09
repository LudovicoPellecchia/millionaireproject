<script>


export default {
    components:{
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
    

    <div class="transform typewriter">

        <h1 class="title"><span class="hidden-text">DO</span> <span class="hidden-text">YOUR</span> <span
                class="hidden-text">QUIZ!</span></h1>
    </div>
</template>

<style lang="scss" scoped>
.transform {
    display: flex;
    justify-content: center;
    padding-top: 30px;
    transform: skewY(-4deg);
}

.hidden-text {
    opacity: 0;
}

span:nth-child(1) {

    align-self: flex-start;
    animation:
        typing 1s steps(40, ),
        blink-caret 1.5s step-end forwards,
        show-text forwards
}

span:nth-child(2) {
    align-self: center;
    animation:
        typing 1s 1s steps(40, end),
        blink-caret 2s 1.5s step-end forwards,
        show-text 0s 1.5s forwards
}

span:nth-child(3) {
    align-self: flex-end;
    animation:
        typing 1s 2s steps(40, end),
        blink-caret 2s 2.5s step-end infinite,
        show-text 0s 2.5s forwards
}

.title {
    width: 50%;
    display: flex;
    flex-direction: column;
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


.typewriter h1 span {

    overflow: hidden;
    /* Ensures the content is not revealed until the animation */
    border-right: .07em solid white;
    /* The typwriter cursor */

    /* Gives that scrolling effect as the typing happens */
    letter-spacing: .07em;
    /* Adjust as needed */


}

/* The typing effect */
@keyframes typing {
    from {
        width: 0
    }

    to {
        width: 50%;
    }
}

/* The typewriter cursor effect */
@keyframes blink-caret {

    from,
    to {
        border-color: transparent
    }

    50% {
        border-color: white;
    }
}

@keyframes show-text {
    to {
        opacity: 1;
    }
}
</style>