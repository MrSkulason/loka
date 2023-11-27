<script>


export default {
  data() {
    return {
      matter: [0, [1, 1], [0]],
      interval: null,
      //baseB[0] = base amount, baseB[1] = total baseBs, baseB[2] = powerOf, baseB[3] multiplier, baseB[4] powerOf, 10 bought, cost multplier
      baseB: [[0,1,1], [0, 0], [1, 0]],
      secondB: [[0,2,3], [0, 0], [1, 0]],
      thirdB: [[0,3,4], [0, 0], [1, 0]],
      fourthB: [[0,4,6], [0, 0], [1, 0]],
      fifthB: [[0,5,8], [0, 0], [1, 0]],
      sixthB: [[0,6,10], [0, 0], [1, 0]],
      prettyNumber: [],
      //list in list to increase
      perSec: [[0, 0],[0, 0],[0, 0],[0, 0],[0, 0],[0, 0]]
    }
  },

  methods: {
    buying(number, number2){
      if(number[1][1] >= number2[0][2]) {
        number[1][0]=number[1][0]-Math.pow(10, number2[0][2]-number[1][1]);
        if (number[1][0] < 0){number[1][0] = 0}

        this.matter[1] = this.powerOf(number[1][0], number[1][1])
        return this.increase1(number2)
      }
      return number2

    },

    increase1: function (increased) {

      increased[1][0] = increased[1][0]+Math.pow(10 ,(-increased[1][1]));

      increased[0][0]++;
      if (increased[0][0]%10 == 0){
        increased[2][0]=increased[2][0]*2;
        increased[0][2] += increased[0][1]
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
      console.log(this.matter)

      return this.powerOf(perSec[0], perSec[1])

    },
    increase(number, number2) {

      if (number[1][1]-number2[1] > 10){return [number[1][0], number[1][1]]}
      else if (number[1][1]-number2[1] < -10){return [number2[1][0], number2[1]]}
      else {number[1][0] = number[1][0] + (number2[0]*(Math.pow(10,number2[1]-number[1][1])))}

        return this.powerOf(number[1][0], number[1][1])
      },

    powerOf(mainNumber, powerOf){

      if((mainNumber >= 10 || (mainNumber < 1)) && mainNumber>0) {
        let TruePowerOf = Math.floor(Math.log10(mainNumber))
        powerOf += TruePowerOf
        console.log(mainNumber)
        mainNumber = mainNumber*Math.pow(10, -TruePowerOf)
      }
      mainNumber = Number(mainNumber.toFixed(4));

      return [mainNumber, powerOf]
    },
    //Number1 = mass
    prettyNumb(number){
      number = Math.floor(number*100)/100
      return number
    }
  },

  mounted() {

    if (localStorage.getItem("matter") != null) {
      this.matter = JSON.parse(localStorage.getItem("matter"))
      this.baseB = JSON.parse(localStorage.getItem("first"))
      this.secondB = JSON.parse(localStorage.getItem("second"))
      this.thirdB = JSON.parse(localStorage.getItem("third"))
      this.fourthB = JSON.parse(localStorage.getItem("fourth"))
      this.fifthB = JSON.parse(localStorage.getItem("fifth"))
      this.sixthB = JSON.parse(localStorage.getItem("sixth"))
    }

    this.interval = setInterval(() => {
      localStorage.setItem("matter", JSON.stringify(this.matter));
      localStorage.setItem("first", JSON.stringify(this.baseB));
      localStorage.setItem("second", JSON.stringify(this.secondB));
      localStorage.setItem("third", JSON.stringify(this.thirdB));
      localStorage.setItem("fourth", JSON.stringify(this.fourthB));
      localStorage.setItem("fifth", JSON.stringify(this.fifthB));
      localStorage.setItem("sixth", JSON.stringify(this.sixthB));
    }, 30000)
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

<div class="absolute inset-0 w-full flex items-center justify-end">
  <p class="text-white">{{prettyNumber[0]}}e{{matter[1][1]}}</p>
  <div class="flex flex-col w-1/3  ml-64 mr-24">

    <div :class="{'[&:not(:hover)]:bg-lime-500 hover:bg-lime-600': matter[1][1] >= baseB[0][2]}" class="bg-white rounded text-black p-4 flex justify-between  mb-7  relative hover:bg-gray-300" @click="this.baseB = buying(this.matter, this.baseB)">

      <div  class="relative top-1/2 left-0 "> Inner Singularity </div>
      <div class="relative top-1/2 left-0 right-0 ">1e{{baseB[0][2]}}</div>
      <div class="flex relative top-1/2  right-0 ">
        <div>{{prettyNumber[1]}}e{{baseB[1][1]}}</div>
        <div class="ml-2">{{prettyNumber[2]}}e{{baseB[2][1]}}</div>

    </div>
    </div>
    <div :class="{ '[&:not(:hover)]:bg-lime-500 hover:bg-lime-600': matter[1][1] >= secondB[0][2]}"  class="bg-white rounded text-black p-4 flex justify-between mb-7 hover:bg-gray-300" @click="this.secondB = buying(this.matter, this.secondB)">
      <div class="relative top-1/2 left-0 "> Inner Singularity </div>
      <div class="relative top-1/2 left-0 right-0 ">1e{{secondB[0][2]}}</div>
      <div class="flex  relative top-1/2  right-0 ">
        <div>{{prettyNumber[3]}}e{{secondB[1][1]}}</div>
        <div class="ml-2">{{prettyNumber[4]}}e{{secondB[2][1]}}</div>
      </div>
    </div>

    <div :class="{ '[&:not(:hover)]:bg-lime-500 hover:bg-lime-600': matter[1][1] >= thirdB[0][2]}" class="bg-white rounded text-black p-4 flex justify-between mb-7 hover:bg-gray-300" @click="this.thirdB = buying(this.matter, this.thirdB)">
      <div class="relative top-1/2 left-0 "> Inner Singularity </div>
      <div class="relative top-1/2 left-0 right-0 ">1e{{thirdB[0][2]}}</div>
      <div class="flex relative top-1/2  right-0 ">
        <div>{{prettyNumber[5]}}e{{thirdB[1][1]}}</div>
        <div class="ml-2">{{prettyNumber[6]}}e{{thirdB[2][1]}}</div>
      </div>
    </div>
    <div :class="{ '[&:not(:hover)]:bg-lime-500 hover:bg-lime-600': matter[1][1] >= fourthB[0][2]}" class="bg-white rounded text-black p-4 flex justify-between mb-7 hover:bg-gray-300" @click="this.fourthB = buying(this.matter, this.fourthB)">
      <div class="relative top-1/2 left-0 "> Inner Singularity </div>
      <div class="relative top-1/2 left-0 right-0 ">1e{{fourthB[0][2]}}</div>
      <div class="flex relative top-1/2  right-0 ">
        <div>{{prettyNumber[7]}}e{{fourthB[1][1]}}</div>
        <div class="ml-2">{{prettyNumber[8]}}e{{fourthB[2][1]}}</div>
      </div>
    </div>
    <div :class="{ '[&:not(:hover)]:bg-lime-500 hover:bg-lime-600': matter[1][1] >= fifthB[0][2]}" class="bg-white rounded text-black p-4 flex justify-between mb-7 hover:bg-gray-300" @click="this.fifthB = buying(this.matter, this.fifthB)">
      <div class="relative top-1/2 left-0 "> Inner Singularity </div>
      <div class="relative top-1/2 left-0 right-0 ">1e{{fifthB[0][2]}}</div>
      <div class="flex relative top-1/2  right-0 ">
        <div>{{prettyNumber[9]}}e{{fifthB[1][1]}}</div>
        <div class="ml-2">{{prettyNumber[10]}}e{{fifthB[2][1]}}</div>
      </div>
    </div>
    <div :class="{ '[&:not(:hover)]:bg-lime-500 hover:bg-lime-600': matter[1][1] >= sixthB[0][2]}" class="bg-white rounded text-black p-4 flex justify-between mb-7 hover:bg-gray-300" @click="this.sixthB = buying(this.matter, this.sixthB)">
      <div class="relative top-1/2 left-0 "> Inner Singularity </div>
      <div class="relative top-1/2 left-0 right-0 ">1e{{sixthB[0][2]}}</div>
      <div class="flex relative top-1/2  right-0 ">
        <div>{{prettyNumber[11]}}e{{sixthB[1][1]}}</div>
        <div class="ml-2">{{prettyNumber[12]}}e{{sixthB[2][1]}}</div>
      </div>
    </div>
  </div>
  </div>




</template>
