<script>
import axios from 'axios';
import CategoriesComp from './CategoriesComp.vue';

export default {
    components: {
        CategoriesComp
    },

    data() {
        return {
            quizSettings: {
                category:"",
                topic: "",
                difficulty: "",
            },

            showMenu: false,
            success: null,
            errors: null

        }
    },
    methods: {
        onFormSubmit() {

            axios
                .post("http://localhost:8000/api/messages", this.quizSettings)
                .then((response) => {
                    this.success = response.data.message;
                    this.errors = null;
                })
                .catch((error) => {
                    this.errors = error.response?.data?.message ?? error.message;
                });
        },

        toggleMenu() {
            this.showMenu = !this.showMenu

            this.$emit('clickedMenu', this.showMenu);

        }
    }
}
</script>


<template>
    <div class="container">
        <div class="settings mt-3 ">

            <div class="setting-title" @click="toggleMenu" :class="{ 'setting-title-active': showMenu }">
                Genera il tuo quiz
                <i v-if="!showMenu" class="arrow-icon fa-solid fa-chevron-down fs-6"></i>
                <i v-if="showMenu" class="arrow-icon fa-solid fa-chevron-up fs-6"></i>
            </div>

            <div v-if="showMenu" class="dropdown-menu" :class="{ 'dropdown-menu-animation': showMenu }">
                <form @submit.prevent="onFormSubmit" class="form-quiz-settings">

                    <div class="form-section-wrapper container">
                        <div class="row row-cols-2">
                            <div class="col my-col">
                                <div class="mb-3">
                                    <div class="label-wrapper">
                                        <label>Scegli una categoria
                                            <i class="fa-solid fa-circle-info"></i>
                                        </label>
                                    </div>

                                    <CategoriesComp></CategoriesComp>
                                    <div class="label-wrapper">
                                        <label>Inserisci l'argomento
                                            <i class="fa-solid fa-circle-info"></i>
                                        </label>
                                    </div>

                                    <input type="text" class="form-control input-text" v-model="quizSettings.topic" />
                                </div>
                            </div>

                            <div class="col">
                                <div class="mb-3">
                                    <div class="label-wrapper">
                                        <label>Seleziona la difficoltà</label>
                                    </div>
                                    <div class="form-check form-check-inline">
                                        <input class="form-check-input" type="radio" name="inlineRadioOptions"
                                            id="inlineRadio1" value="option1">
                                        <label class="form-check-label" for="inlineRadio1">Facile</label>
                                    </div>
                                    <div class="form-check form-check-inline">
                                        <input class="form-check-input" type="radio" name="inlineRadioOptions"
                                            id="inlineRadio2" value="option2">
                                        <label class="form-check-label" for="inlineRadio2">Intermedio</label>
                                    </div>
                                    <div class="form-check form-check-inline">
                                        <input class="form-check-input" type="radio" name="inlineRadioOptions"
                                            id="inlineRadio3" value="option3">
                                        <label class="form-check-label" for="inlineRadio3">Difficile</label>
                                    </div>
                                </div>


                                <div class="mb-3">
                                    <label>Seleziona la Lingua</label>
                                    <input type="text" class="form-control" v-model="quizSettings.topic" />
                                </div>
                            </div>
                        </div>


                    </div>
                    <div class="btn-wrapper text-center">
                        <button type="submit" class="btn my-btn mb-3 mt-3">Genera</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.settings {
    display: inline-block;
    position: relative;
    z-index: 3;
}

.setting-title {
    padding: 15px 25px;
    border-radius: 20px;
    background-color: rgba(255, 255, 255, 0.147);
    font-family: 'Anonymous Pro', monospace;
    font-size: 1.2rem;
    display: inline-block;
    height: 100%;
    color: white;
    cursor: pointer;
    opacity: 0.5;
    transition: opacity 0.4s;
    border: 1px solid transparent;


    &:hover {
        opacity: 1;
    }
}

.setting-title-active {
    opacity: 1;
    border: 1px solid rgba(196, 35, 102, 0.494);
    box-shadow: 0px 0px 6px rgb(196, 35, 102);
}

.arrow-icon {
    margin-left: 5px;
}

.dropdown-menu {
    border: 1px solid rgba(196, 35, 102, 0.494);
    box-shadow: 0px 0px 6px rgb(196, 35, 102);
    color: white;
    display: block;
    position: fixed;
    width: 90%;
    max-width: 800px;
    background-color: rgba(37, 52, 64, 0.745);
    border-radius: 20px;
    margin-top: 5px;


    .form-quiz-settings {
        padding: 15px;

        .label-wrapper{
            text-align: center;
        }

        label {
            text-align: center;
            display: inline-block;
            margin-bottom: 5px;
            position: relative;

            i {
                color: rgba(255, 255, 255, 0.619);
                font-size: 0.8rem;
                position: absolute;
                top: 0;
                right: -20px;
            }
        }

        .input-text {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            box-sizing: border-box;
        }

    }

    .my-col {
        border-right: 2px solid rgba(196, 35, 102, 0.494);
    }


    .form-check-input:checked {
        background-color: rgb(112, 92, 242);
        border-color: rgb(112, 92, 242);
    }
}

.dropdown-menu-animation {
    top: 50%;
    left: 50%;

    animation: growDown 400ms ease-in-out forwards;

}

@keyframes growDown {
    0% {

        transform: scaleY(0) translate(-50%, -50%);
    }

    80% {

        transform: scaleY(1.1) translate(-50%, -50%);
    }

    100% {

        transform: scaleY(1) translate(-50%, -50%);
    }
}

.my-btn {
    display: inline-block;
    color: white;
    background-color: rgb(112, 92, 242);

    &:hover {
        background-color: rgb(112, 92, 242);

    }
}
</style>
