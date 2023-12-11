<script>
import axios from 'axios';

export default {

    data() {
        return {
            quizSettings: {
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
        }
    }
}
</script>


<template>
    <div class="container">
        <div class="settings mt-3">

            <div class="setting-title" @click="toggleMenu" :class="{ 'setting-title-active': showMenu }">
                Genera il tuo quiz
                <i v-if="!showMenu" class="arrow-icon fa-solid fa-chevron-down fs-6"></i>
                <i v-if="showMenu" class="arrow-icon fa-solid fa-chevron-up fs-6"></i>
            </div>

            <div v-if="showMenu" class="dropdown-menu" :class="{ 'dropdown-menu-animation': showMenu }">
                <form @submit.prevent="onFormSubmit" class="form-quiz-settings">
                    <div class="mb-3">
                        <label>Inserisci l'argomento</label>
                        <input type="text" class="form-control" v-model="quizSettings.topic" />
                    </div>
                    <div class="mb-3">
                        <label>Seleziona la difficoltà</label>
                        <input type="text" class="form-control" v-model="quizSettings.topic" />
                    </div>
                    <button type="submit" class="btn my-btn mb-3">Genera</button>
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

    color: white;
    display: block;
    position: fixed;
    width: 100%;
    max-width: 800px;
    background-color: rgb(37, 52, 64);
    border-radius: 20px;
    margin-top: 5px;
    margin-right:30px ;
    margin-left:30px ;

    .form-quiz-settings {
        padding: 15px;

        label {
            display: block;
            margin-bottom: 5px;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            box-sizing: border-box;
        }

        button {
            width: 100%;
        }
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
    color: white;
    background-color: rgb(112, 92, 242);

    &:hover {
        background-color: rgb(112, 92, 242);

    }
}</style>
