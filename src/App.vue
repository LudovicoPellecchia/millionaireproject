

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

    }
  }
}
</script>


<template>
  <div class="container">
    <PromptComp></PromptComp>
    <TitleComp></TitleComp>
    <ContenitoreComp></ContenitoreComp>
  </div>
</template>

<style lang="scss">

</style>
