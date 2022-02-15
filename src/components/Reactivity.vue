<template>
  <div>{{name}}</div>
  <div>{{getName()}}</div>
  <div>{{sayHello()}}</div>
  <div>{{upperCaseName}}</div>
  <button @click="changeName()">ay mmgvo</button>
</template>
<script>
// re-renderiza
export default {
  data() {
    return {
      name: 'emiles'
    }
  },
  methods: {
    getName(){
      return this.name
    },
    changeName () {
      this.name = 'guillermo'
    },
    sayHello () {
      return 'hola'
    }
  },
  computed: {
    upperCaseName(){
      return this.name.toUpperCase()
    }
  },
  
  beforeCreate(){},
  created(){},
  beforeMount(){},
  mounted() {
    // hacer llamados a APIS
    // suscribirte a canales o eventos
    console.log('hi')
  },
  updated(){},
  beforeUpdate(){},
  beforeUnmount(){},
  unmounted(){
    // desuscribirte a canales o eventos
    console.log('destroyed')
  }
}
</script>
