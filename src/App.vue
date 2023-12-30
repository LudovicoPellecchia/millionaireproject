

<script>
import ContenitoreComp from './components/ContenitoreComp.vue';
import TitleComp from './components/TitleComp.vue';
import PromptComp from './components/PromptComp.vue'
import LoaderComp from './components/LoaderComp.vue';


export default {
  components: {
    ContenitoreComp,
    TitleComp,
    PromptComp,
    LoaderComp
  },

  data() {
    return {
      quiz:[],
      blurredBody: null,
      loaderQuiz: false

    }
  },
  methods: {
    blurBody() {
      this.blurredBody = !this.blurredBody
    },
    generateQuiz(quiz, loadingQuiz){
      this.$refs.ContenitoreComp.restartQuiz();
      this.loaderQuiz = loadingQuiz
      this.quiz = quiz
      this.blurredBody = null
    },

    showLoader(loadingQuiz){
      this.loaderQuiz = loadingQuiz

    }

  }
}
</script>


<template>
  <div class="body-wrapper" :class="{ 'blur-bg': blurredBody, 'not-blur' : !blurredBody, 'loader-active': loaderQuiz} " >

    <div class="container">
      <PromptComp @clickedMenu="blurBody" @generatedQuiz="generateQuiz" @loadingQuiz="showLoader"></PromptComp>
      <TitleComp :class="{ 'blur': blurredBody, 'not-blur' : !blurredBody }"></TitleComp>
      <ContenitoreComp :class="{ 'blur': blurredBody, 'not-blur' : !blurredBody }" :quiz="quiz" ref="ContenitoreComp"></ContenitoreComp>
      <LoaderComp class="loader-position" :class="{'loader-style' : loaderQuiz}"></LoaderComp>

    </div>
  </div>
</template>

<style lang="scss">

.body-wrapper{
  position: relative;
  height: 100vh;

  .loader-position{
    opacity: 0;
    position: absolute;
    bottom: 15px;
    right: 50%;
    transform: translate(50%, -50%);
  }


  .loader-style{
    animation: showOpacity 1s forwards;
  }

  @keyframes showOpacity {
    0% {
            opacity: 0;
        }

        100% {
            opacity: 1;
        }
  }

  
}

.loader-active{
    pointer-events:none;
  }

.blur {
  transition: filter 0.5s;
  filter: blur(8px);
}
.blur-bg{
  transition: backdrop-filter 0.5s;

  backdrop-filter: blur(8px);
}
.not-blur{
  filter: blur(0);
  transition: filter 0.5s, backdrop-filter 0.5s;
  backdrop-filter: blur(0);
}
</style>
