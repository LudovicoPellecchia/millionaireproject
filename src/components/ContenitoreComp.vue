<script>
import axios from 'axios';
import DomandaComp from './DomandaComp.vue';
import RisposteComp from './RisposteComp.vue';
import RestartBtn from './RestartBtn.vue';

export default {
  components: {
    DomandaComp,
    RisposteComp,
    RestartBtn
  },

  data() {
    return {
      quiz: [],
      usedQuestions: [],
      questionIndex: null,
      finishedQuiz: false
    }
  },

  methods: {
    fetchQuiz() {

      axios.get('quiz.json').then((response) => {

        this.quiz = response.data;
      })
    },

    fetchRandomQuestion() {
      do {
        this.questionIndex = Math.floor(Math.random() * this.quiz.length);
      } while (this.usedQuestions.includes(this.questionIndex));

      this.usedQuestions.push(this.questionIndex);
      console.log(this.usedQuestions);

      return this.questionIndex;
    },



    async fetchNextQuestion(selectedOption) {
      const correctAnswer = this.quiz[this.questionIndex].rispostaCorretta;

      if (selectedOption === correctAnswer) {
        // Opzione selezionata corretta, incrementa questionIndex
        this.fetchRandomQuestion();

        // Verifica se ci sono altre domande nel quiz
        if (this.usedQuestions.length < 1) {
          await this.fetchQuiz(); // Effettua la chiamata axios solo dopo aver incrementato questionIndex
          // Puoi anche aggiungere ulteriori azioni o logiche necessarie qui
        } else {
          // Se hai finito tutte le domande, puoi gestire la logica di fine quiz qui
          this.finishedQuiz = true
        }
      } else {
        // Opzione selezionata errata, puoi gestire la logica degli errori qui se necessario
        console.log('Risposta errata, puoi gestire gli errori qui.');
      }
    },


    restartQuiz() {
      this.usedQuestions =[];
      this.finishedQuiz = false;
      this.questionIndex = this.fetchRandomQuestion();
    }
  },



  mounted() {
    this.fetchRandomQuestion()
    this.fetchQuiz()
  }
}
</script>


<template>
  <div v-if="!finishedQuiz">
    <DomandaComp :quiz="quiz[questionIndex]"></DomandaComp>
    <RisposteComp :quiz="quiz[questionIndex]" @optionSelected="fetchNextQuestion"></RisposteComp>
  </div>


  <div v-else>
    <div class="text-center">Hai terminato il quiz</div>
    <RestartBtn  @click="restartQuiz()"></RestartBtn>
  </div>
</template>

<style lang="scss" scoped>

</style>
