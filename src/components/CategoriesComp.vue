<script>

export default {

    data() {
        return {
            categories: [

                { nome: "Matematica", backgroundColor: "rgb(173, 216, 230)", placeholder: "Esempio: Equazioni algebriche" },
                { nome: "Scienze", backgroundColor: "rgb(144, 238, 144)", placeholder: "Esempio: Il ciclo dell'acqua" },
                { nome: "Storia", backgroundColor: "rgb(221, 160, 221)", placeholder: "Esempio: La rivoluzione francese" },
                { nome: "Tecnologia", backgroundColor: "rgb(255, 182, 193)", placeholder: "Esempio: Introduzione a JavaScript" },
                { nome: "Lingue", backgroundColor: "rgb(255, 228, 181)", placeholder: "Esempio: Grammatica italiana" },
                { nome: "Letteratura", backgroundColor: "rgb(255, 239, 184)", placeholder: "Esempio: Opere di Shakespeare" },
                { nome: "Arte, Musica e Spettacolo", backgroundColor: "rgb(204, 204, 255)", placeholder: "Esempio: Impressionismo" },
                { nome: "Geografia", backgroundColor: "rgb(244, 164, 96)", placeholder: "Esempio: Le capitali del mondo" },
                { nome: "Scienze Sociali", backgroundColor: "rgb(176, 224, 230)", placeholder: "Esempio: Psicologia sociale" },
                { nome: "Filosofia", backgroundColor: "rgb(192, 192, 192)", placeholder: "Esempio: Teoria dell'etica" },
                { nome: "Sport", backgroundColor: "rgb(173, 216, 230)", placeholder: "Esempio: Regole del calcio" },
                { nome: "Religione", backgroundColor: "rgb(240, 216, 230)", placeholder: "Esempio: Le grandi religioni" }


            ],
            currentIndex: 0,
            itemsPerPage: 5,
            activeBadge: null,

        }
    },
    computed: {
        totalSlides() {
            return Math.ceil(this.categories.length / this.itemsPerPage);
        },

        visibleCategories() {
            const start = this.currentIndex * this.itemsPerPage;
            const end = start + this.itemsPerPage;
            return this.categories.slice(start, end);
        },
    },
    methods: {
        nextSlide() {
            if (this.currentIndex < this.totalSlides - 1) {
                this.currentIndex++;
            }
        },
        prevSlide() {
            if (this.currentIndex > 0) {
                this.currentIndex--;
            }
        },

        selectedCategory(option) {
            this.activeBadge = option

            this.$emit('selectedCategory', option);

        }
    },
};
</script>


<template>
    <div class="slider-wrapper">
        <i class="fa-solid fa-chevron-up arrow-up" @click="prevSlide"
            :class="(currentIndex === 0) ? 'transparence-i' : ''"></i>

        <div class="badge-container">
            <div class="badge-wrapper text-center" v-for="(category) in visibleCategories" :key="category.name">
                <div class="badge-style" :style="{ 'background-color': category.backgroundColor }"
                    @click="selectedCategory(category)" :class="{ 'badge-style-active': activeBadge === category }">
                    {{ category.nome }}
                </div>
            </div>
        </div>

        <i class="fa-solid fa-chevron-down arrow-down" @click="nextSlide"
            :class="(currentIndex === totalSlides - 1) ? 'transparence-i' : ''"></i>
    </div>
</template>


<style lang="scss" scoped>
.slider-wrapper {
    padding: 10px 0;
    position: relative;

    i:hover {
        cursor: pointer;
    }

    .arrow-up {
        position: absolute;
        top: 0;
        left: 50%;
        transform: translate(-50%);
    }

    .arrow-down {
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translate(-50%);
    }

    .transparence-i {
        color: rgba(255, 255, 255, 0.393);
    }
}

.badge-container {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin: 10px 0;

}

.badge-wrapper {
    padding: 0 20px;
}


.badge-style {
    border: 2px solid transparent;
    box-shadow: 0px 0px 6px transparent;

    color: rgba(0, 0, 0, 0.391);
    text-align: center;
    font-size: 0.9rem;
    padding: 8px 12px;
    border-radius: 40px;


    &:hover {
        cursor: pointer;
        color: black;
        transition: color 0.5s;
    }
}

.badge-style-active {
    color: black;
    font-weight: 500;
    box-shadow: 0px 0px 6px rgb(196, 35, 102);
    border: 2px solid rgb(196, 35, 102);

}
</style>