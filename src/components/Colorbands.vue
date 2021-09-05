<template>
  <div>
    <div class="block">
      <h1> Select component type </h1>
      <div class="buttons">
        <button class="button" v-on:click="countBands = 3" v-bind:class="{'is-info': countBands == 3}"> 3 Band Resistor </button>
        <button class="button" v-on:click="countBands = 4" v-bind:class="{'is-info': countBands == 4}"> 4 Band resistor </button>
        <button class="button" v-on:click="countBands = 5" v-bind:class="{'is-info': countBands == 5}"> 5 Band resistor </button>
        <button class="button" v-on:click="countBands = 6" v-bind:class="{'is-info': countBands == 6}"> 6 Band resistor </button>
        <button class="button" v-on:click="countBands = -4" v-bind:class="{'is-info': countBands == -4}"> 4 Band inductor </button>
      </div>
    </div>
    <div class="block">
      <Colortable v-bind:bands="currbands()" v-on:tableChange="dispCalc" />
    </div>

    <div> <!-- Results -->
			<span> {{getResistance()}} </span>
		</div>

  </div>
</template>

<script>
import Colortable from './reusables/Colortable.vue'

export default {
  name: 'Colorbands',
  components: {
    Colortable
  },
  props: {
    
  },
  data(){return{
    tbldata: [],
    countBands: 0,
    bandsData: [
      {names:['1st Digit', '2nd Digit', 'Multiplier'], colors:['0123456789','0123456789','0123456789AB']},
      {names:['1st Digit', '2nd Digit', 'Multiplier', 'Tolerance'], colors:['0123456789','0123456789','0123456789AB', '0123456789AB']},
      {names:['1st Digit', '2nd Digit', '3rd Digit', 'Multiplier', 'Tolerance'], colors:['0123456789','0123456789', '0123456789','0123456789AB', '0123456789AB']}
    ]
  }},
  methods:{
    dispCalc(tbl){
      this.tbldata = tbl;
    },
    currbands(){
      if(this.countBands == 3) return this.bandsData[0];
      else if(this.countBands == 4) return this.bandsData[1];
      else if(this.countBands == 5) return this.bandsData[2];
    },
    getResistance(){
      function getDigits(ndigit){
        var p = [1, 10, 100, 1000];
        if (ndigit == -1) return ['m', 100];
        else if (ndigit == -2) return ['m', 10];
        else if(ndigit < 3) return ['', p[ndigit]];
        else if (ndigit < 6) return ['k', p[ndigit-3]];
        else if (ndigit < 9) return ['M', p[ndigit-6]];
        else if (ndigit < 12) return ['G', p[ndigit-9]];
        
      }
      if(this.countBands == 3){
        if(! this.isTableFilled(3)) return "N/A"
        var r = parseInt(this.tbldata[0]) * 10 + parseInt(this.tbldata[1])
        var mul = this.tbldata[2];
        console.log(this.tbldata[2]); // debug
        if(mul == 'A') mul = -1;
        else if (mul == 'B') mul == -2;
        else mul = parseInt(mul);
        console.log(mul);
        return `${r} E ${mul} = ${r*getDigits(mul)[1]}${getDigits(mul)[0]}`;
      }
    },
    isTableFilled(len){
      if(this.tbldata.length < len) return false;
      for(var each in this.tbldata){
        if (this.tbldata[each] == null) return false;
      }
      return true;
    }
  }
}
</script>
