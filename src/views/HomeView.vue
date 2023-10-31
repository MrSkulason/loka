<script>


export default {
  data() {
    return {
      matter: [5, 0],
      interval: null,
      //baseB[0] = base amount, baseB[1] = total baseBs, baseB[2] = powerOf, baseB[3] multiplier, baseB[4] powerOf
      baseB: [0, [0, 0], [1, 0]],
      secondB: [0, [0, 0], [1, 0]],
      prettyNumber: [],
      //list in list to increase
      perSec: [[],[],[]]
    }
  },
  methods: {
    increase1: function (increased) {

      increased[1][0] = increased[1][0]+Math.pow(10 ,(-increased[1][1]));

      increased[0]++;
      if (increased[0]%10 == 0){
        increased[2][0]=increased[2][0]*2;
      }
      increased[1] = this.powerOf(increased[1][0], increased[1][1])

      increased[2] = this.powerOf(increased[2][0], increased[2][1])
      this.baseB = increased
    },
    perSecond(number){
      let perSec = [0, 0]
      perSec[0]= number[1][0]*number[2][0]
      perSec[1]=number[1][1]+number[2][1]
      console.log(perSec)
      return this.powerOf(perSec[0], perSec[1])
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
      if(mainNumber >= 10 || mainNumber < 1) {
        let TruePowerOf = Math.floor(Math.log10(mainNumber))
        powerOf += TruePowerOf
        console.log(mainNumber)
        mainNumber = mainNumber/Math.pow(10, TruePowerOf)
      }
      mainNumber = Math.floor((mainNumber*10000))/10000

      return [mainNumber, powerOf]
    },
    //Number1 = mass
    prettyNumb(number){
      number = Math.floor(number*100)/100
      return number
    }
  },

  mounted() {
    this.interval = setInterval(() => {}, 100)
    this.interval = setInterval(() => {
      //mass
      this.perSec[0] = this.perSecond(this.baseB),
      this.matter = this.increase(this.matter[0], this.perSec[0]),
      //increases BaseB
      this.perSec[1] = this.perSecond(this.secondB),
      this.matter = this.increase(this.baseB[1], this.perSec[1])
    }, 100)
    this.interval = setInterval(() => {
      this.prettyNumber[0] = this.prettyNumb(this.matter[0]),
      this.prettyNumber[1] = this.prettyNumb(this.baseB[1][0]),
      this.prettyNumber[2] = this.prettyNumb(this.baseB[2][0]),
      this.prettyNumber[3] = this.prettyNumb(this.baseB[0])
    }, 100)

  }
}

</script>

<template>
  <p class="text-white">{{prettyNumber[0]}}e{{matter[1]}}</p>

  <button class="bg-white rounded text-black p-4" @click="increase1(this.baseB)">Inner Singularity {{prettyNumber[1]}}e{{baseB[1][1]}} {{prettyNumber[2]}}e{{baseB[2][1]}}</button>



</template>
