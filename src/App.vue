<template>
  <div id="app" class="container">
    <div>
      <h1 class="title is-1"> Resistor Calculator </h1>
    </div>
    
    <div class="field has-addons">
      <p class="control">
        <button class="button is-outlined is-link" v-on:click="view = 'bands'"> Color Bands </button>
      </p>
      <p class="control">
        <button class="button is-outlined is-link" v-on:click="view = 'digit'"> Digits </button>
      </p>
    </div>

    <div v-if="view == 'bands'">
      <Colorbands   />
    </div>

    <div v-if="view == 'empty' ">
      <p> Select Type of marking on the part to continue. </p>
    </div>
    
  </div>
</template>

<script>
import Colorbands from './components/Colorbands.vue'

export default {
  name: 'App',
  components: {
    Colorbands
  },
  data(){return{
    view: 'empty',
  }}
}

</script>

<style>

</style>
