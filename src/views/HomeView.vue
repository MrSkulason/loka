<script>


export default {
  data() {
    return {
      matter: [0, [5, 0], [0]],
      interval: null,
      //baseB[0] = base amount, baseB[1] = total baseBs, baseB[2] = powerOf, baseB[3] multiplier, baseB[4] powerOf
      baseB: [0, [0, 0], [1, 0]],
      secondB: [0, [0, 0], [1, 0]],
      thirdB: [0, [0, 0], [1, 0]],
      fourthB: [0, [0, 0], [1, 0]],
      fifthB: [0, [0, 0], [1, 0]],
      sixthB: [0, [0, 0], [1, 0]],
      prettyNumber: [],
      //list in list to increase
      perSec: [[0, 0],[0, 0],[0, 0],[0, 0],[0, 0],[0, 0]]
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
      return increased
    },
    perSecond(number){
      let perSec = [0, 0]
      perSec[0]= number[1][0]*number[2][0]
      perSec[1]=number[1][1]+number[2][1]
      console.log(number)
      console.log(perSec)
      return this.powerOf(perSec[0], perSec[1])
    },
    increase(number, number2) {

      if (number[1][1]-number2[1] > 10){return [number[1][0], number[1][1]]}
      else if (number[1][1]-number2[1] < -10){return [number2[1][0], number2[1]]}
      else {number[1][0] = number[1][0] + (number2[0]*(Math.pow(10,number2[1]-number[1][1])))}

        return this.powerOf(number[1][0], number[1][1])
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
      this.matter[1] = this.increase(this.matter, this.perSec[0])
      console.log(this.perSec)
      //increases BaseB
      this.perSec[1] = this.perSecond(this.secondB),
      this.baseB[1] = this.increase(this.baseB, this.perSec[1])
      //increases BaseB
      this.perSec[2] = this.perSecond(this.thirdB),
      this.secondB[1] = this.increase(this.secondB, this.perSec[2])
      //increases BaseB
      this.perSec[3] = this.perSecond(this.fourthB),
      this.thirdB[1] = this.increase(this.thirdB, this.perSec[3])
      //increases BaseB
      this.perSec[4] = this.perSecond(this.fifthB),
      this.fourthB[1] = this.increase(this.fourthB, this.perSec[4])
      //increases BaseB
      this.perSec[5] = this.perSecond(this.sixthB),
      this.fifthB[1] = this.increase(this.fifthB, this.perSec[5])
    }, 100)
    this.interval = setInterval(() => {
      this.prettyNumber[0] = this.prettyNumb(this.matter[1][0]),
      this.prettyNumber[1] = this.prettyNumb(this.baseB[1][0]),
      this.prettyNumber[2] = this.prettyNumb(this.baseB[2][0]),
      this.prettyNumber[3] = this.prettyNumb(this.secondB[1][0]),
      this.prettyNumber[4] = this.prettyNumb(this.secondB[2][0]),
      this.prettyNumber[5] = this.prettyNumb(this.thirdB[1][0]),
      this.prettyNumber[6] = this.prettyNumb(this.thirdB[2][0]),
      this.prettyNumber[7] = this.prettyNumb(this.fourthB[1][0]),
      this.prettyNumber[8] = this.prettyNumb(this.fourthB[2][0]),
      this.prettyNumber[9] = this.prettyNumb(this.fifthB[1][0]),
      this.prettyNumber[10] = this.prettyNumb(this.fifthB[2][0]),
      this.prettyNumber[11] = this.prettyNumb(this.sixthB[1][0]),
      this.prettyNumber[12] = this.prettyNumb(this.sixthB[2][0])
    }, 100)

  }
}

</script>

<template>
  <p class="text-white">{{prettyNumber[0]}}e{{matter[1][1]}}</p>

  <button class="bg-white rounded text-black p-4" @click="this.baseB = increase1(this.baseB)">Inner Singularity {{prettyNumber[1]}}e{{baseB[1][1]}} {{prettyNumber[2]}}e{{baseB[2][1]}}</button>
  <button class="bg-white rounded text-black p-4" @click="this.secondB = increase1(this.secondB)">Second {{prettyNumber[3]}}e{{secondB[1][1]}} {{prettyNumber[4]}}e{{secondB[2][1]}}</button>
  <button class="bg-white rounded text-black p-4" @click="this.thirdB = increase1(this.thirdB)">Second {{prettyNumber[5]}}e{{thirdB[1][1]}} {{prettyNumber[6]}}e{{thirdB[2][1]}}</button>
  <button class="bg-white rounded text-black p-4" @click="this.fourthB = increase1(this.fourthB)">Second {{prettyNumber[7]}}e{{fourthB[1][1]}} {{prettyNumber[8]}}e{{fourthB[2][1]}}</button>
  <button class="bg-white rounded text-black p-4" @click="this.fifthB = increase1(this.fifthB)">Second {{prettyNumber[9]}}e{{fifthB[1][1]}} {{prettyNumber[10]}}e{{fifthB[2][1]}}</button>
  <button class="bg-white rounded text-black p-4" @click="this.sixthB = increase1(this.sixthB)">Second {{prettyNumber[11]}}e{{sixthB[1][1]}} {{prettyNumber[12]}}e{{sixthB[2][1]}}</button>





</template>
