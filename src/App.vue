<template>
  <div id="app">
    <GamePanel />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import GamePanel from './components/GamePanel.vue'

@Component({
  components: {
    GamePanel
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.css';
@import '~bulma/bulma.sass';
@import '~buefy/dist/buefy.css';
@import '~animate.css/animate.css';

body {
  background-color: #bad1cd;
  color: #253031;
  font-size: 22pt;
}
</style>
