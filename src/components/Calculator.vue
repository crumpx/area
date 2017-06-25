<template lang="html">
  <content>
    <div class="container">

      <div class="box">
        <p>轉小數<br>Fraction to decimal</p>
        <input class='decimal-input' type="text" name="" v-model="numerator"><span>/</span>
        <input class='decimal-input' type="text" name="" v-model="denominator" >
        <p>{{fraction}}</p>
      </div>
      <div class="box">
        <p>算面積<br>Calculato area</p>
        <div v-for='input, index in inputs'>
          <span>{{index + 1}}. </span>
          <input type="text" placeholder="" v-model="input.parm1" >
          <input type="text" placeholder="" v-model="input.parm2" v-if="!inputs[index+1]" v-on:click.once="addInput(index)">
          <input type="text" placeholder="" v-model="input.parm2" v-else v-on:click="calThis(index)">
          <p >{{input.res}} ft<span class='sqf'>2</span></p>
          <!-- <button type="button" name="button" v-if="!inputs[index+1]" v-on:click.once="addInput(index)">Add</button> -->
        </div>


      </div>

      <div class="">
        <button type="button" name="button" v-on:click="getResult()">總數/total</button>
        <button type="button" name="button" v-on:click="reset()">重置/reset</button>
      </div>
      <div class="">
        <p>{{result}} ft<span class='sqf'>2</span></p>
      </div>
      </div>


    </content>
</template>

<script>
export default {
  name: 'calculator',
  data() {
    return {
      inputs: [{parm1: '', parm2: '', res: 0}],
      result: 0,
      numerator: 1,
      denominator: 16,

    }
  },
  computed: {
    fraction: function(){
      return this.numerator / this.denominator
    },
  },
  methods: {
    addInput: function (index) {
      this.inputs[index].res = this.inputs[index].parm1 * this.inputs[index].parm2 / 144
      this.inputs.push({parm1:'', parm2:'',res: 0})
    },
    calThis: function(index) {
      this.inputs[index].res = this.inputs[index].parm1 * this.inputs[index].parm2 / 144
    },
    reset: function() {
      this.inputs= [{parm1: '', parm2: '', res: 0}]
    },
    getResult: function() {
      var inputsLength = this.inputs.length
      if (this.inputs[inputsLength-1].parm1 && this.inputs[inputsLength-1].parm2 && this.inputs[inputsLength-1].res == 0){
        this.inputs[inputsLength-1].res = this.inputs[inputsLength-1].parm1 * this.inputs[inputsLength-1].parm2 / 144
      }
      this.result = 0
      for (var i=0; i<this.inputs.length; i++) {
        if (this.inputs[i].parm1 === '' || this.inputs[i].parm2 ==='') {
          this.inputs.splice(i, 1)
        }
      this.result += this.inputs[i].res;
      }
    },
  }
}
</script>

<style lang="css">
  input {
    width: 20%;
    margin: 6px 5px;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid black;
    text-align: center;
  }
  p {
    margin: 4px 0
  }
  input:focus {
    border: none;
    border-radius: 5px;
  }

  button {
    padding: 10px 14px;
    margin: 10px 0;
  }

  .container {
    width: 320px;
    margin: 0 auto;
  }
  .box {
    border: 1px solid black;
    border-radius: 4px;
    padding: 5px 10px;
    margin: 5px 0
  }
  .sqf {
    font-size: 70%;
    vertical-align: text-top;
  }

  .decimal-input {
    width: 10%;
  }

</style>
