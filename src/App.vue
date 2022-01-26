
<template>
 <!-- here i am calling my views -->
<div id="app" class="app">
  <ActiveCard v-if="activetab === 1" :created="created" @sendtab="tabData"/>
  <AddCard v-else @send="addcard"/>
</div>
</template>

<script>
import AddCard from './view/AddCard'
import ActiveCard from './view/ActiveCard'
  function sendDataLocalStorage(data){
  localStorage.setItem("cardData", JSON.stringify(data))
  }
  function getData(){
  let data = localStorage.getItem("cardData")
  return data
  }
export default {
  components: {
    AddCard,
    ActiveCard,
    },
  data(){
    //localStorage.removeItem("cardData");
    return{
      activetab: 1,
      card:[],
        cardnumber:'',
        name:'',
        month:'',
        year: '',
        vendor:'',
    }
  },
  computed:{
    created(){
    let data = localStorage.getItem("cardData")
    if(data){
      [...this.card] = JSON.parse(data)
    }
    return this.card
    },
    data(){
      return this.activetab
    }
  },
  methods:{
    tabData(sendtab){
      this.activetab = sendtab
      return this.activetab
    },
    addcard(cardData){
       let obj =[]
        obj = getData()
        if(obj){
       obj= JSON.parse(obj)
       let nycount = [...obj]
       for (const cardN of nycount) {
         if(cardN.cardnumber === cardData.cardnumber){
           alert("You have allready card with same Number. You can not add this")
           return 
         }
       }
          // let counter =0
          // let i = 0
          // for ( i = 0; i < nycount.length; i++) {
          // if (nycount[i].vendor) 
          // counter++;
          // }
          // if(counter >= 4)
          // {
          // alert("Your limt of cards in wallet is full now. you want to Uppdate  first one card and save this one")
          // // alert(cardData.vendor)
          // // alert(nycount)
          // const result = nycount.filter(word => word.vendor != cardData.vendor);
          // //alert(result)
          // this.card = result
          // // alert(this.card)
          // sendDataLocalStorage(this.card)
          // }
       //alert(counter)
        }
      this.card.push({
        cardnumber: cardData.cardnumber,
        name: cardData.name,
        month: cardData.month,
        year: cardData.year,
        vendor:cardData.vendor
      })
      sendDataLocalStorage(this.card)
      this.activetab =1
    }
  }

}
</script>

<style >
#app{
  display: grid;
  justify-content: center;
  background-color: cadetblue;
}
</style>
