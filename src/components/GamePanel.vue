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
      mode="out-in"
    >
      <div class="slide slide-0" v-if="displaySlide(0)"></div>

      <DisclaimerSlide v-if="displaySlide(1)" />

      <WelcomeSlide v-if="displaySlide(2)" />

      <QuestionPanel
        :questions="nextSet"
        :count="questionCount"
        @selected="addQuestion"
        @next="nextQuestion"
        v-if="displaySlide(3)"
      ></QuestionPanel>

      <div class="slide" v-if="displaySlide(4)">
        <div class="slide-content">
          <h3>Autre questions</h3>
          <ol>
            <li v-for="(question, ndx) in questions" :key="ndx">
              {{ question }}
            </li>
          </ol>
        </div>
      </div>

      <div class="slide" v-if="displaySlide(5)">
        <div class="slide-content has-text-centered">
          <h3>Credit</h3>
          <ul>
            <li>Animateur : Moi ............... Sébastien Lafleur</li>
            <li>Invité : Moi ............... Sébastien Lafleur</li>
            <li>Producteur : Moi ............... Sébastien Lafleur</li>
            <li>Animation : Moi ............... Sébastien Lafleur</li>
            <li>Camera : Vous ............... Assistance</li>
          </ul>

          <h3>Making of</h3>
          <p>40+ heures de programmation.</p>
        </div>
      </div>

      <div class="slide" v-if="displaySlide(6)">
        <div class="slide-content has-text-centered">
          <h1>Merci</h1>
        </div>
      </div>
    </transition>

    <button class="button is-primary is-outlined slide-control next-slide" v-if="currentSlide < 6" @click="nextSlide">
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
  public questionCount: number = 1
  public questions: string[] = [
    'Quel est ton parcours professionnel ?',
    'Quel est ton parcours scolaire ?',
    'Comment as-tu décidé de devenir programmeur ?',
    'Comment en es-tu venu a être un "fan" de lutte ?',
    "À l'exception du badminton, est-ce que tu pratiques d'autres sports ?",
    'Est-ce que tu es un "gamer" ?',
    'Quel sont tes séries télévision préférer ?',
    'Quel sont tes films préférer ?',
    'Est-ce que tu as des livres que tu préfères ?',
    'Quel est ton type de cuisine préférer ?',
    'Autre intérêt en informatique ?',
    "Qu'est ce que tu aimerais le plus accomplir en informatique ?",
    'Pourquoi les cheveux longs ?',
    'Quel serait ton voyage de rêve ?',
    'Quelle activité la plus extravagante que tu aimerais faire ?',
    'Pourquoi ton aversion pour les vacances ?',
    'Quel de tes sens pourrais-tu accepter de perdre ?',
    'Est-ce que tu as des phobies ?',
    'Quel est ton genre de musique préférer ?'
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
    this.currentSlide = min([++this.currentSlide, 6])
    e.target.blur()
  }

  public addQuestion(questions: string[]): void {
    this.questions = this.questions.concat(questions)
  }

  public nextQuestion(): void {
    this.questionCount++
    if (this.questionCount > 10) {
      return
    }
    this.nextSet = this.createSubset()
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
