<template>
  <div class="slide">
    <div class="slide-content" v-if="count < 11">
      <h3>{{ count }}. Choisir une porte</h3>
      <div class="options-container">
        <transition-group
          tag="ul"
          name="custom-classes-transition"
          enter-active-class="animated zoomIn"
          leave-active-class="animated zoomOut"
        >
          <li v-for="(question, key) in currentQuestions()" :key="key" @click="openDoor(key)">
            <div class="columns options">
              <div class="column is-1 small">{{ key + 1 }}</div>
              <div class="column" style="position: relative">
                <div class="door-mask"></div>
                {{ question }}
              </div>
            </div>
          </li>
        </transition-group>

        <transition
          name="custom-classes-transition"
          enter-active-class="animated zoomInDown"
          leave-active-class="animated hinge"
        >
          <div v-if="hasSelection" style="height: 100%; position: relative;">
            {{ selected }}
            <button class="button is-primary is-outlined" @click="nextQuestion">Suivant</button>
          </div>
        </transition>
      </div>
    </div>

    <div class="slide-content" v-else>
      <h3>Il s'agit du temps maximum que nous avons pour cette émission. Merci de votre participation !</h3>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Emit, Prop, Vue, Watch } from 'vue-property-decorator'

@Component
export default class QuestionPanel extends Vue {
  @Prop({ default: (): string[] => [] })
  public questions!: string[]

  @Prop()
  public count!: number

  public selected: string = ''
  public hasSelection: boolean = false

  @Watch('selected')
  public currentQuestions(): string[] {
    return this.selected ? [] : this.questions
  }

  @Watch('questions')
  public updateHasSelection(): void {
    this.selected = ''
    this.hasSelection = false
  }

  @Emit('selected')
  public openDoor(ndx: number): string[] {
    const questions = this.questions.slice(0)
    this.selected = questions.splice(ndx, 1)[0]
    setTimeout(() => {
      this.hasSelection = true
    }, 500)
    return questions
  }

  @Emit('next')
  public nextQuestion(e: any): boolean {
    e.target.blur()
    return true
  }
}
</script>

<style lang="scss" scoped>
.options-container {
  height: 400px;
  position: relative;

  button {
    position: absolute;
    bottom: 0;
    right: 0;
  }
}

.slide {
  .slide-content {
    height: 450px;
    
    .options {
      margin: 15px 0;
      background-color: #7a7978;
      border-radius: 10px;
      padding: 5px 0;
      height: 100px;
    
      .column.small {
        width: 70px;
        text-align: center;
        border-right: 2px solid #000;
      }
    }
  }
}

.door-mask {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  opacity: 1;
  height: 100%;
  width: 100%;
  background-color: #7a7978;
}
</style>
