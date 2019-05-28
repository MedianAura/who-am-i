<template>
  <div class="slide">
    <div class="slide-content" @click="increaseNdx">
      <h2 class="has-text-centered">Bienvenue au show Vigilance ...</h2>
      <h1 class="has-text-centered" :class="{ visible: ndx >= 1 }">Qui suis-je ?</h1>
      <p class="has-text-centered" :class="{ visible: ndx >= 2 }">
        Votre animateur :
        <span :class="{ visible: ndx >= 3 }">... Moi ?</span>
      </p>
      <p class="has-text-centered" :class="{ visible: ndx >= 4 }">
        L'invité spécial :
        <span :class="{ visible: ndx >= 5 }">... Moi ?</span>
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { min } from 'lodash'

@Component
export default class WelcomeSlide extends Vue {
  public ndx: number = 0

  public increaseNdx(): void {
    this.ndx = min([++this.ndx, 5])
  }
}
</script>

<style scoped lang="scss">
.slide-content {
  cursor: pointer;
  h1 {
    opacity: 0;
    &.visible {
      opacity: 1;
      transition: opacity 0.6s ease;
    }
  }

  p {
    opacity: 0;

    &.visible {
      opacity: 1;
      transition: opacity 0.3s ease;
    }
  }

  span {
    opacity: 0;

    &.visible {
      opacity: 1;
      transition: opacity 0.6s ease;
    }
  }
}
</style>
