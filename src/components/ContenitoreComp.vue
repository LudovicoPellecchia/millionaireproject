<script>
import axios from 'axios';
import DomandaComp from './DomandaComp.vue';
import RisposteComp from './RisposteComp.vue';
import RestartBtn from './RestartBtn.vue';
import ProgressBar from './ProgressBar.vue'

export default {
  components: {
    DomandaComp,
    RisposteComp,
    RestartBtn,
    ProgressBar
  },

  data() {
    return {
      quiz: [],
      usedQuestions: [],
      questionIndex: null,
      finishedQuiz: false,
      progress: 0,
      failedQuiz: false
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
      console.log(this.usedQuestions)


      return this.questionIndex;
    },



    async fetchNextQuestion(selectedOption) {
      const correctAnswer = this.quiz[this.questionIndex].rispostaCorretta;

      const handleCorrectAnswer = async () => {
        this.failedQuiz = false;
        // Opzione selezionata corretta, trova un random questionIndex
        this.fetchRandomQuestion();
        // Dopo ogni domanda risposta correttamente
        this.progress += 0.1;
        // Verifica se il quiz ha raggiunto il termine
        if (this.usedQuestions.length < 11) {
          await this.fetchQuiz(); // Effettua la chiamata axios solo dopo aver incrementato questionIndex
          // Puoi anche aggiungere ulteriori azioni o logiche necessarie qui
        } else {
          // Se hai finito il quiz
          this.finishedQuiz = true;
        }
      };

      const handleWrongAnswer = () => {
        // Opzione selezionata errata, puoi gestire la logica degli errori qui se necessario
        this.progress = 0;
        this.usedQuestions = [];
        this.questionIndex = this.fetchRandomQuestion();
        this.failedQuiz = true;
        console.log('Risposta errata, puoi gestire gli errori qui.');
      };

      // Ritarda l'esecuzione della funzione di 1 secondo
      setTimeout(() => {
        if (selectedOption === correctAnswer) {
          handleCorrectAnswer();
        } else {
          handleWrongAnswer();
        }
      }, 1500);
    },



    restartQuiz() {
      this.failedQuiz = false
      this.progress = 0;
      this.usedQuestions = [];
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
  <ProgressBar :progress="progress"></ProgressBar>

  <div v-if="failedQuiz">
    Risposta sbagliata
    <RestartBtn @click="restartQuiz()"></RestartBtn>
  </div>

  <div v-if="!finishedQuiz && !failedQuiz">
    <DomandaComp :quiz="quiz[questionIndex]"></DomandaComp>
    <RisposteComp :quiz="quiz[questionIndex]" @optionSelected="fetchNextQuestion"></RisposteComp>
  </div>

  <div v-if="finishedQuiz">
    <div class="text-center">Hai terminato il quiz</div>
    <RestartBtn @click="restartQuiz()"></RestartBtn>
  </div>
</template>

<style lang="scss" scoped></style>
