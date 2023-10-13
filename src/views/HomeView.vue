<script>


export default {
  data() {
    return {
      matter: [5, 0],
      interval: null,
      multiplier1: 1,
      baseAmount1: 0,
      amount1: 0,
      persec: 0
    }
  },
  methods: {
    increase1: function () {
      this.amount1++;
      this.baseAmount1++;
      if (this.baseAmount1%10 == 0){
        this.multiplier1=this.multiplier1*2;
      }
    },
    increase(number, number2) {
      if (number[1]-number2[1] > 10){this.powerOf(number[0], number[1])}
      else if (number[1]-number2[1] < -10){this.powerOf(number2[0], number[1])}
      number[0] = number[0] + (number2[0]*(10^(number2[1]-number[1])))
      return this.powerOf(number[0], number[1])
      },

    stopInterval() {
      clearInterval(this.interval);
    },
    powerOf(mainNumber, powerOf){
      if(mainNumber > 10 || mainNumber < 1) {
        let TruePowerOf = Math.floor(Math.log10(mainNumber))
        powerOf += TruePowerOf

        mainNumber = mainNumber/(10^TruePowerOf)
      }
      return [mainNumber, powerOf]
    }
  },
  mounted() {
    this.interval = setInterval(() => {this.persec = this.amount1 * this.multiplier1}, 1000)
    this.interval = setInterval(() => {this.matter[0] = this.matter[0] + this.persec}, 1000)
  }
}

</script>

<template>
  <p class="text-white">{{matter[0]}}e{{matter[1]}}</p>

  <button class="bg-white rounded text-black p-4" @click="increase1">Inner Singularity {{amount1}} {{multiplier1}}</button>



</template>
