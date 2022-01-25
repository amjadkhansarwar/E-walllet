<template>
<div id="app">
  <ActiveCard v-if="activetab === 1" :created="created" @sendtab="tabData"/>
  <AddCard v-else @send="addcard"/>
  <AddData />
</div>
</template>

<script>
import AddCard from './component/AddCard'
import AddData from './view/AddData'
import ActiveCard from './component/ActiveCard'
function sendDataLocalStorage(data){
  localStorage.setItem("cardData", JSON.stringify(data))
}
function count(){
      let data = localStorage.getItem("cardData")
      if(data){
        return data
      }
    }
export default {
  components: {
    AddCard,
    ActiveCard,
    AddData
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
      console.log(cardData);
      let validcard =cardData.cardnumber.toString().length
      if(validcard < 16 || validcard > 16 ){
        alert("You must put  only 16 digits for card number if you want to register it")
        return
      }
       let obj =[]
       let counter =0
       obj = count()
       let i = 0
       obj= JSON.parse(obj)
       let nycount = [...obj]
       for (const cardN of nycount) {
         if(cardN.cardnumber === cardData.cardnumber){
           alert("You have allready card with same Number. You can not add this")
           return 
         }
       }
        for ( i = 0; i < nycount.length; i++) {
        if (nycount[i].vendor) 
           counter++;
        }
        if(counter >= 4)
        {
         alert("Your limt of cards in wallet is full now. you want to delete first one card and save this one")
         alert(cardData.vendor)
         alert(nycount)
         const result = nycount.filter(word => word.vendor != cardData.vendor);
         alert(result)
         this.card = result
          alert(this.card)
          sendDataLocalStorage(this.card)
        }
       alert(counter)
      this.card.push({
        cardnumber: cardData.cardnumber,
        name: cardData.name,
        month: cardData.month,
        year: cardData.year,
        vendor:cardData.vendor
      }),
      sendDataLocalStorage(this.card)
      this.activetab =1
    }
  }

}
</script>

<style >
#app{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
