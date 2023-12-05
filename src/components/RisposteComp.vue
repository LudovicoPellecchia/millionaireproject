<script>

export default {

    props: {
        quiz: Object
    },

    data() {
        return {
            selectedOption: null,
            hoveredOption: null,
            fadeAnimationActive: false,
            hoverMouseLeave: false,
            hoverMouseOver: false
        }
    },

    methods: {
        selectOption(option) {
            const isCorrect = option === this.quiz?.rispostaCorretta;
            this.selectedOption = isCorrect ? option : null;

            if (isCorrect) {
                this.fadeAnimationActive= false,
                this.hoverMouseLeave= false
                this.activateAnimation();
            }

            this.$emit('optionSelected', option, isCorrect);
        },


        activateAnimation() {
            this.fadeAnimationActive = true;
            // Disabilita l'animazione dopo un certo periodo
            setTimeout(() => {
                this.fadeAnimationActive = false;
            }, 1500); // Imposta la durata dell'animazione in millisecondi
        },

        leaveHoverAnimation(option) {
            this.hoveredOption = option 
            this.hoverMouseLeave = true
            this.hoverMouseOver = false
        },

        startHoverAnimation(option){
            this.hoveredOption = option 
            this.hoverMouseOver = true
            this.hoverMouseLeave = false


        }

    }
}
</script>


<template>
    <div class="container my-style-container">
        <div class="row row-cols-2 gy-3">
            <div class="col d-flex justify-content-center" v-for="opzione in quiz?.opzioni" :key="opzione">
                <div class="item" @mouseleave="leaveHoverAnimation(opzione)" @mouseover="startHoverAnimation(opzione)" @click="selectOption(opzione)" :class="{
                    'correct-answer': selectedOption === opzione,
                    'fade-animation': selectedOption !== opzione && fadeAnimationActive,
                    'no-hover': fadeAnimationActive,
                    'leave-mouse-hover': hoveredOption === opzione && hoverMouseLeave &&!hoverMouseOver,
                    'start-mouse-hover': hoveredOption === opzione && hoverMouseOver &&!hoverMouseLeave,
                }">
                    {{ opzione }}
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.item {
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
/*     transition: transform 0.5s;
 */



    &:hover {
/*         transform: scale(1.06);
 */        animation: tilt-shaking 0.4s infinite 0.4s ease-in-out;

        @keyframes tilt-shaking {
            0% {
                transform: scale(1.06) rotate(0deg);
            }

            25% {
                transform: scale(1.06) rotate(0.5deg);
            }

            50% {
                transform: scale(1.06)rotate(0eg);
            }

            75% {
                transform: scale(1.06) rotate(-0.5deg);
            }

            100% {
                transform: scale(1.06) rotate(0deg);
            }
        }
    }
}

.no-hover {
    pointer-events: none;
}

.start-mouse-hover {
    transition: transform 0.4s;
    transform: scale(1.06);


/*     animation: scaling-up 0.2s ease;

    @keyframes scaling-up {
        from {
            transform: scale(1);
        }

        to {
            transform: scale(1.06);
        }
    } */

    
}


.leave-mouse-hover {
    animation: scaling-out 0.4s ease;

    @keyframes scaling-out {
        from {
            transform: scale(1.06)
        }

        to {
            transform: scale(1);
        }
    }

}

.fade-animation {
    animation: fade-out 0.4s linear forwards; // Aggiunto "forwards" per mantenere l'ultimo stato dell'animazione

    @keyframes fade-out {
        0% {
            transform: translateX(0);
            opacity: 1;
        }

        100% {
            transform: translateX(100px);
            opacity: 0;
        }
    }
}



.correct-answer {
    background-color: #B1CC74 !important;
    transition: background-color 200ms;

}
</style>