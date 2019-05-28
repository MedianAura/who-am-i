<template>
  <div class="slide">
    <div class="slide-content">
      <h3>Choisir une porte</h3>
      <ul>
        <li v-for="(question, key) in questions" :key="key" @click="openDoor(key)">
          <div class="columns options">
            <div class="column is-1 small">{{ key + 1 }}</div>
            <div class="column">
              <div style="position: relative">
                <div class="door-mask"></div>
                {{ question }}
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Emit, Prop, Vue } from 'vue-property-decorator'

@Component
export default class QuestionPanel extends Vue {
  @Prop({ default: (): string[] => [] })
  public questions!: string[]

  @Emit('selected')
  public openDoor(ndx: number): string[] {
    const questions = this.questions.slice(0)
    questions.splice(ndx, 1)
    return questions
  }
}
</script>

<style lang="scss" scoped>
  .slide .slide-content .options {
    margin: 15px 0;
    background-color: #7A7978;
    border-radius: 10px;
    padding: 5px 0;
    
    .column.small {
      width: 70px;
      text-align: center;
      border-right: 2px solid #000;
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
    background-color: #7A7978;
  }
</style>
