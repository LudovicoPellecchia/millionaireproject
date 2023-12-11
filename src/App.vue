

<script>
import ContenitoreComp from './components/ContenitoreComp.vue';
import TitleComp from './components/TitleComp.vue';
import PromptComp from './components/PromptComp.vue'


export default {
  components: {
    ContenitoreComp,
    TitleComp,
    PromptComp
  },

  data() {
    return {
      blurredBody: null

    }
  },
  methods: {
    blurBody() {
      this.blurredBody = !this.blurredBody
    }

  }
}
</script>


<template>
  <div class="body-wrapper" :class="{ 'blur-bg': blurredBody, 'not-blur' : !blurredBody}" >

    <div class="container">
      <PromptComp @clickedMenu="blurBody"></PromptComp>
      <TitleComp :class="{ 'blur': blurredBody, 'not-blur' : !blurredBody }"></TitleComp>
      <ContenitoreComp :class="{ 'blur': blurredBody, 'not-blur' : !blurredBody }"></ContenitoreComp>
    </div>
  </div>
</template>

<style lang="scss">
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
