<script>


export default {
  data() {
    return {
      matter: 5,
      active: true
    }
  },
  methods: {
    
    increase: function () {



    }
  }
}

</script>

<template>
  <p class="text-white">{{matter}}</p>

  <button class="bg-white rounded text-black p-4" @click="increase">Increase</button>



</template>
