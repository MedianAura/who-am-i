<template>
  <div class="slide">
    <div class="slide-content" @click="increaseNdx">
      <h2>Disclaimer :</h2>
      <ol>
        <li :class="{ visible: ndx >= 1 }">Il n'y aura aucun photo dans cette présentation.</li>

        <li :class="{ visible: ndx >= 2 }">La présence de faute d'orthographe est une possibilité.</li>

        <li :class="{ visible: ndx >= 3 }">Je ne tiens pas tant que ça a devenir camionneur.</li>

        <li :class="{ visible: ndx >= 4 }">
          Moi et Serge pourrions surement nous recycler cependant comme propriétaire du Shack : Bob la Patate
        </li>
      </ol>
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
    this.ndx = min([++this.ndx, 4])
  }
}
</script>

<style scoped lang="scss">
.slide-content {
  cursor: pointer;

  ol {
    li {
      opacity: 0;
    }

    li.visible {
      opacity: 1;
      transition: opacity 0.3s ease;
    }
  }
}
</style>
