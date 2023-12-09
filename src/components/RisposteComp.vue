<script>

export default {

    props: {
        quiz: Object
    },

    data() {
        return {
            selectedOption: null,
            hoveredOption: null,
            correctAnimationActive: false,
            wrongAnimationActive: false,
            hoverMouseLeave: false,
            hoverMouseOver: false,
            leaveHoverTimeout: null,
            startHoverTimeout: null,
            isWrong: false,
            isCorrect: false
        }
    },

    methods: {
        selectOption(option, index) {
            this.selectedOption = option

            this.isCorrect= this.selectedOption === this.quiz?.rispostaCorretta;
            this.isWrong = this.selectedOption !== this.quiz?.rispostaCorretta && this.selectedOption === this.quiz?.opzioni[index];

            if (this.isCorrect) {
                this.correctAnswerAnimation();
            }
            if (this.isWrong) {
                this.wrongAnswerAnimation();
            }


            this.$emit('optionSelected', option, this.isCorrect, this.isWrong );
        },


        correctAnswerAnimation() {
            this.correctAnimationActive = true;
            // Disabilita l'animazione dopo un certo periodo
            setTimeout(() => {
                this.isCorrect= false
                this.correctAnimationActive = false;
            }, 1500); // Imposta la durata dell'animazione in millisecondi
        },

        wrongAnswerAnimation(){
            this.wrongAnimationActive = true;
            // Disabilita l'animazione dopo un certo periodo
            setTimeout(() => {
                this.isWrong = false
                this.wrongAnimationActive = false;
            }, 1500); // Imposta la durata dell'animazione in millisecondi
        },


        leaveHoverAnimation(option) {
        // Cancella eventuali timeout precedenti
        clearTimeout(this.leaveHoverTimeout);

        this.leaveHoverTimeout = setTimeout(() => {
            this.hoveredOption = option;
            this.hoverMouseLeave = true;
            this.hoverMouseOver = false;
        }, 20); // Imposta la durata dell'animazione in millisecondi
    },

    startHoverAnimation(option) {
        // Cancella eventuali timeout precedenti
        clearTimeout(this.startHoverTimeout);

        this.startHoverTimeout = setTimeout(() => {
            this.hoveredOption = option;
            this.hoverMouseOver = true;
            this.hoverMouseLeave = false;
        }, 2); // Imposta la durata dell'animazione in millisecondi
    }

    }
}
</script>


<template>
    <div class="container my-style-container">
        <div class="row row-cols-2 gy-3">
            <div class="col d-flex justify-content-center" v-for="(opzione, index) in quiz?.opzioni" :key="opzione">
                <div class="item" @mouseleave="leaveHoverAnimation(opzione)" @mouseover="startHoverAnimation(opzione)"
                    @click="selectOption(opzione, index)" :class="{
                        'correct-answer': selectedOption === opzione && isCorrect || (opzione === quiz?.rispostaCorretta && isWrong) ,
                        'wrong-answer' : selectedOption === opzione && isWrong,
                        'fade-animation': selectedOption !== opzione && correctAnimationActive,
                        'opacity-animation': selectedOption !== opzione && wrongAnimationActive && (opzione !== quiz?.rispostaCorretta && isWrong),
                        'no-hover': correctAnimationActive || wrongAnimationActive,
                        'leave-mouse-hover': hoveredOption === opzione && hoverMouseLeave && !hoverMouseOver,
                        'start-mouse-hover': hoveredOption === opzione && hoverMouseOver && !hoverMouseLeave,
                    }">
                    {{ opzione }}
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Anonymous+Pro);

.item {
    font-family: 'Anonymous Pro', monospace;
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
 */
        animation: tilt-shaking 0.4s infinite 0.4s ease-in-out;

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

}


.leave-mouse-hover {
    transition: transform 0.4s;
    transform: scale(1);
}


.fade-animation {
    animation: fade-out 0.4s  linear forwards; // Aggiunto "forwards" per mantenere l'ultimo stato dell'animazione

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

.opacity-animation{
    opacity: 0;
    transition: opacity 1s 0.5s;
}

.correct-answer {
    background-color: #B1CC74 !important;
    transition: background-color 200ms;
}
.wrong-answer {
    background-color: rgb(211, 69, 69) !important;
    transition: background-color 200ms;
}
</style>