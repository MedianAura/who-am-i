<template>
  <div>
    <GamePanel :questions="nextSet" @selected="addQuestion"></GamePanel>

    <div class="slide slide-0" v-if="displaySlide(0)"></div>

    <div class="slide" v-if="displaySlide(1)">
      Disclaimer
    </div>

    <div class="slide" v-if="displaySlide(1)">
      Il n'y aura aucun photo dans cette présentation.
    </div>

    <div class="slide" v-if="displaySlide(1)">
      La présence de faute d'orthographe est une possibilité.
    </div>

    <div class="slide" v-if="displaySlide(1)">
      Qui suis-je ?
    </div>

    <div class="slide" v-if="displaySlide(1)">
      Votre animateur ... Moi ?
    </div>

    <div class="slide" v-if="displaySlide(1)">
      L'invité spécial ... Moi ?
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { shuffle, take } from 'lodash'
import GamePanel from '@/components/GamePanel.vue'

@Component({
  components: { GamePanel }
})
export default class HelloWorld extends Vue {
  public currentSlide: number = 0
  public questions: string[] = [
    'Quel est ton parcours professionnel ?',
    'Quel est ton parcours scolaires ?',
    'Comment as tu décidé de devenir programmeur ?',
    'Lutte ?',
    "A part du badminton, est ce que tu pratique d'autre sport ?",
    'Passe temps : Jeux vidéo ?',
    'Passe temps : Télévisuel ?',
    '8',
    '9',
    '10',
    '11',
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

  public changeSlide(): void {
    this.currentSlide++
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

<style scoped lang="scss">
.slide {
  height: 100vh;
  display: flex;
  align-items: center;

  &.slide-0 {
    background-color: #000000;
  }
}
</style>
