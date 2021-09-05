<template>
	<div id="cp">
		<table class="table is-bordered is-narrow">
			<thead bgcolor="#c0c0c0">
				<td v-for="(name, index) in bands.names"> 
					<p> band {{index}} </p>
					<p>{{ name }} </p>
				</td>
			</thead>
			<tbody id="tbody">
				<td v-for="(color, index) in bands.colors">					
					<tr v-for="each in tolist(color)">
						<td>
							<input type="radio" v-bind:id="`radio${each}-${index}`" v-bind:value="each" v-model="selects[index]" v-on:click="sendCalc()">
							<label v-bind:for="`radio${each}-${index}`" class="radio" v-bind:style="{color: toColor(each)}"> <b>{{toColor(each)}}</b> </label>
						</td>
					</tr>
				</td>
			</tbody>
		</table>

	</div>
</template>

<script>
export default {
	name: 'Colortable',
	props:{
		bands: {
			type: Object,
			default: () => {
				return {names: [], colors: []}
			}
		}
	},
	methods:{
		// Resistor table methods
		toColor(ch){
			var colorArr = [
					'black', 'brown', 'red', 'orange', 'yellow', 'green',
					'blue', 'violet', 'grey', 'white', 'gold', 'silver'
			]
			var i;

			if(ch == 'A') i=10;
			else if(ch == 'B') i=11;
			else i=parseInt(ch);

			return colorArr[i];
		},
		tolist(str){
			var s = String(str);
			return s.split('');
		},
		// Pass message methods
		sendCalc(){
			this.$emit('tableChange', this.selects);
		}
	},
	data(){return{
		selects: []
	}}
	
}
</script>

<style scoped>
#tbody {
	background-color:lightskyblue;
}
</style>