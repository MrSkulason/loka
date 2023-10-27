<script>


export default {
  data() {
    return {
      matter: [5, 0],
      interval: null,
      //baseB[0] = base amount, baseB[1] = total baseBs, baseB[2] = powerOf, baseB[3] multiplier, baseB[4] powerOf
      baseB: [0, 0, 0, 1, 0],
      prettyNumber: [],
      perSec: [0, 0]
    }
  },
  methods: {
    increase1: function () {

      this.baseB[1] = this.baseB[1]+Math.pow(10 ,(-this.baseB[2]));

      this.baseB[0]++;
      if (this.baseB[0]%10 == 0){
        this.baseB[3]=this.baseB[3]*2;
      }
      let result = this.powerOf(this.baseB[1], this.baseB[2])
      this.baseB[1] = result[0]
      this.baseB[2] = result[1]
      result = this.powerOf(this.baseB[3], this.baseB[4])
      this.baseB[3] = result[0]
      this.baseB[4] = result[1]
    },
    perSecond(){
      this.perSec[0]=this.baseB[1]*this.baseB[3]
      this.perSec[1]=this.baseB[2]+this.baseB[4]
      console.log(this.perSec)
      return this.powerOf(this.perSec[0], this.perSec[1])
    },
    increase(number, number2) {
      console.log(number)
      console.log(number2)
      console.log(((number[1]-number2[1])))
      if (number[1]-number2[1] > 10){return [number[0], number[1]]}
      else if (number[1]-number2[1] < -10){return [number2[0], number2[1]]}
      else {number[0] = number[0] + (number2[0]*(Math.pow(10,number2[1]-number[1])))}

        return this.powerOf(number[0], number[1])
      },

    stopInterval() {
      clearInterval(this.interval);
    },
    powerOf(mainNumber, powerOf){
      if(mainNumber > 10 || mainNumber < 1) {
        let TruePowerOf = Math.floor(Math.log10(mainNumber))
        powerOf += TruePowerOf
        console.log(mainNumber)
        mainNumber = mainNumber/Math.pow(10, TruePowerOf)
      }
      mainNumber = Math.ceil((mainNumber*10000))/10000

      return [mainNumber, powerOf]
    },
    //Number1 = mass
    prettyNumb(number){
      number = Math.floor(number*100)/100
      return number
    }
  },

  mounted() {
    this.interval = setInterval(() => {this.persec = this.perSecond()}, 100)
    this.interval = setInterval(() => {this.matter = this.increase(this.matter, this.persec) }, 100)
    this.interval = setInterval(() => {
      this.prettyNumber[0] = this.prettyNumb(this.matter[0]),
      this.prettyNumber[1] = this.prettyNumb(this.baseB[1]),
      this.prettyNumber[2] = this.prettyNumb(this.baseB[3]),
      this.prettyNumber[3] = this.prettyNumb(this.matter[0])
    }, 100)
  }
}

</script>

<template>
  <p class="text-white">{{prettyNumber[0]}}e{{matter[1]}}</p>

  <button class="bg-white rounded text-black p-4" @click="increase1">Inner Singularity {{baseB[1]}}e{{baseB[2]}} {{baseB[3]}}e{{baseB[4]}}</button>



</template>
