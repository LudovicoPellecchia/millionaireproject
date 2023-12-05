

<script>
import ContenitoreComp from './components/ContenitoreComp.vue';

export default {
  components: {
    ContenitoreComp
  },

  data() {
    return {

    }
  }
}
</script>


<template>
  <div class="container">
    <div class="text-center ">
      <h1 class="title">Chi vuole essere milionario</h1>
    </div>
    <ContenitoreComp></ContenitoreComp>
  </div>
</template>

<style lang="scss">
.title {
  color: white;
  display: inline-block;
  background-color: #311847;
  margin-bottom: 80px;
  border-radius: 40px;
  padding: 20px 40px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  
}
</style>
