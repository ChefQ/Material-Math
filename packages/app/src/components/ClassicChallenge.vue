<template>
  <div class="container">
    <challenge-streak />
    <classic-question
      class="question"
      :question="question"
    />
    <classic-input />
  </div>
</template>

<script lang="ts">
import ClassicInput from "./ClassicInput.vue";
import ClassicQuestion from "./ClassicQuestion.vue";
import ChallengeStreak from "./ChallengeStreak.vue";
import {
  PracticeActions,
  PracticeGetters,
  PracticeOptions
} from "../store/practice/practice";
import { Operator } from "../engine/math_questions/expression/models";
import { ChallengeType } from "../engine/models/math_question";
import { mapActions, mapGetters } from "vuex";
import Vue from "vue";

export default Vue.extend({
  components: {
    ClassicInput,
    ClassicQuestion,
    ChallengeStreak
  },
  props: {
    challengeTypes: Array as () => Array<ChallengeType>,
    operators: Array as () => Array<Operator>,
    difficulty: String
  },
  mounted() {
    this.initializePractice({
      operators: this.operators,
      difficulty: this.difficulty,
      challengeTypes: this.challengeTypes
    } as PracticeOptions);
    this.newQuestion();
  },
  methods: {
    ...mapActions({
      newQuestion: PracticeActions.NEW_QUESTION,
      initializePractice: PracticeActions.INIT
    }),
    myProperty(): boolean {
      // <- Here
      return true;
    }
  },
  computed: {
    ...mapGetters({
      question: PracticeGetters.QUESTION_LATEX
    })
  }
});
</script>

<style scoped>
.container {
  max-width: 600px;
  max-height: 85%;
}

.question {
  margin: -42px 16px 16px 16px;
}
</style>
