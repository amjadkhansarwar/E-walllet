<template>
  <div>
    <p v-if=" active === 1" >{{message}}</p>
    <p v-if="active ===2" >{{message}}</p>
    <p v-if=" active ===3" >{{message}}</p>
    <p v-if="active ===4" >{{message}}</p>
    
    <button v-on:click="active == 1" >button 1</button>
    <button v-on:click="active == 2" @message1="message">button 2</button>
    <button v-on:click="active == 3" >button 3</button>
    <button v-on:click="active == 4" >button 4</button>
  </div>
</template>

<script>
export default {
  data(){
      return{
    active: 1,
    message: '12',
  }
  },
  method:{
      message1(){
          this.message = 'button 1'
      }
  }
}
</script>

<style>
</style>