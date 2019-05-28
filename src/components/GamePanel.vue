<template>
  <div class="slide">
    <div class="slide-content">
      <h1>Choisir une porte</h1>
      <ul>
        <li v-for="(question, key) in questions" :key="key" @click="openDoor(key)">
          <div class="columns">
            <div class="column is-1">{{ key + 1 }}</div>
            <div class="column">{{ question }}</div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Emit, Prop, Vue } from 'vue-property-decorator'

@Component
export default class GamePanel extends Vue {
  @Prop({ default: () => [] })
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
  .slide-content {
    width: 60%;
    margin: auto;
  }
</style>
