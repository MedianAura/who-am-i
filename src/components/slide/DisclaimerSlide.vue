<template>
  <div class="slide">
    <div class="slide-content" @click="increaseNdx">
      <h2>Disclaimer :</h2>
      <transition-group tag="ol" name="custom-classes-transition" enter-active-class="animated lightSpeedIn">
        <li :key="1" v-if="ndx >= 1">Il n'y aura aucune photo dans cette présentation.</li>

        <li :key="2" v-if="ndx >= 2">La présence de faute d'orthographe est une possibilité.</li>

        <li :key="3" v-if="ndx >= 3">Je ne tiens pas tant que ça à devenir camionneur.</li>

        <li :key="4" v-if="ndx >= 4">
          Moi et Serge pourrions surement nous recycler cependant comme propriétaire du Shack : Bob la Patate.
        </li>

        <li :key="5" v-if="ndx >= 5">
          Chaque fois que je crois avoir une bonne idée pour une présentation. Je trouve une façon de la ruiner...
        </li>
      </transition-group>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { min } from 'lodash'

@Component
export default class DisclaimerSlide extends Vue {
  public ndx: number = 0

  public increaseNdx(): void {
    this.ndx = min([++this.ndx, 5])
  }
}
</script>

<style scoped lang="scss">
.slide-content {
  cursor: pointer;
  height: 500px;
}
</style>
