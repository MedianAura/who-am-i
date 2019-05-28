<template>
  <div>
    <button
      class="button is-primary is-outlined slide-control previous-slide"
      v-if="currentSlide > 0"
      @click="previousSlide"
    >
      <i class="fas fa-angle-double-up"></i>
    </button>

    <transition
      name="custom-classes-transition"
      enter-active-class="animated tada"
      leave-active-class="animated bounceOutRight"
    >
      <div class="slide slide-0" v-if="displaySlide(0)"></div>
    </transition>

    <transition
      name="custom-classes-transition"
      enter-active-class="animated tada"
      leave-active-class="animated bounceOutRight"
    >
      <DisclaimerSlide v-if="displaySlide(1)" />
    </transition>

    <transition
      name="custom-classes-transition"
      enter-active-class="animated tada"
      leave-active-class="animated bounceOutRight"
    >
      <WelcomeSlide v-if="displaySlide(2)" />
    </transition>

    <transition
      name="custom-classes-transition"
      enter-active-class="animated tada"
      leave-active-class="animated bounceOutRight"
    >
      <QuestionPanel :questions="nextSet" @selected="addQuestion" v-if="displaySlide(3)"></QuestionPanel>
    </transition>

    <button class="button is-primary is-outlined slide-control next-slide" v-if="currentSlide < 7" @click="nextSlide">
      <i class="fas fa-angle-double-down"></i>
    </button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { shuffle, min, max } from 'lodash'
import QuestionPanel from '@/components/QuestionPanel.vue'
import DisclaimerSlide from '@/components/slide/DisclaimerSlide.vue'
import WelcomeSlide from '@/components/slide/WelcomeSlide.vue'

@Component({
  components: { QuestionPanel, DisclaimerSlide, WelcomeSlide }
})
export default class GamePanel extends Vue {
  public currentSlide: number = 0
  public questions: string[] = [
    'Quel est ton parcours professionnel ?',
    'Quel est ton parcours scolaires ?',
    'Comment as tu décidé de devenir programmeur ?',
    'Comment en es tu venu a être un fan de lutte ?',
    "A part du badminton, est ce que tu pratique d'autre sport ?",
    'Quel genre de gamer es tu ?',
    'Quel sont tes série télévision préferer ?',
    'Quel sont tes films préferer ?',
    'Est-ce que tu as des livres que tu préfère ?',
    'Quel est ton type de cuisine préferer ?',
    'Autre intérèt en informatique ?',
    '12',
    '13',
    '14',
    '15',
    '16',
    '17',
    '18',
    '19',
    '20'
  ]
  public nextSet: string[] = []

  public mounted(): void {
    this.nextSet = this.createSubset()
  }

  public displaySlide(slide: number): boolean {
    return slide === this.currentSlide
  }

  public previousSlide(e: any): void {
    this.currentSlide = max([--this.currentSlide, 0])
    e.target.blur()
  }

  public nextSlide(e: any): void {
    this.currentSlide = min([++this.currentSlide, 7])
    e.target.blur()
  }

  public addQuestion(questions: string[]): void {
    this.questions = this.questions.concat(questions)
  }

  public createSubset(): string[] {
    for (let i = 0; i < 10; i++) {
      this.questions = shuffle(this.questions)
    }
    return this.questions.splice(0, 3)
  }
}
</script>

<style lang="scss">
.slide {
  height: 100vh;
  display: flex;
  align-items: center;

  &.slide-0 {
    background-color: #000000;
  }

  .slide-content {
    width: 60%;
    margin: auto;

    h1 {
      font-size: 108pt;
      font-family: 'Lakki Reddy', cursive;
      color: #f18f01;
    }

    h2 {
      font-size: 36pt;
      font-family: 'Mogra', cursive;
      color: #048ba8;
    }

    h3 {
      font-size: 30pt;
      font-family: 'Original Surfer', cursive;
      color: #048ba8;
    }
  }
}
</style>

<style lang="scss" scoped>
.slide-control {
  position: absolute;
  width: 200px;
  left: 50%;

  &.next-slide {
    bottom: 0;
    transform: translate(-50%, -50%);
  }

  &.previous-slide {
    top: 0;
    transform: translate(-50%, 50%);
  }
}
</style>
