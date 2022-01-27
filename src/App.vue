
<template>
 <!-- here i am calling my views -->
<div id="app" class="app">
  <ActiveCard v-if="activeView === 1" :created="created" @sendViewData="viewData"/>
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
          activeView: 1,
          card:[
            {
            cardnumber:'2222 3333 4444 5555',
            name:'Amjad',
            month:'09',
            year: '22',
            vendor:'Evil',
            }
            ],
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
          return this.activeView
        }
      },
      methods:{
        viewData(sendViewData){
          this.activeView = sendViewData
          return this.activeView
        },
        addcard(cardData){

      // checking Card number duplication 

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
                    //  Uppdate card or Deleteing duplicate card with respect to vendor
                // let counter =0
                // let i = 0
                // for ( i = 0; i < nycount.length; i++) {
                // if (nycount[i].vendor) 
                // counter++;
                // }
                // if(counter >= 4)
                // {
                // alert("Your limt of cards in wallet is full now. you want to Uppdate  first one card and save this one")
                // const result = nycount.filter(word => word.vendor != cardData.vendor);
                // this.card = result
                // sendDataLocalStorage(this.card)
                // }
          }
           // Adding Data in local storage

            this.card.push({
            cardnumber: cardData.cardnumber,
            name: cardData.name,
            month: cardData.month,
            year: cardData.year,
            vendor:cardData.vendor
            })
            sendDataLocalStorage(this.card)
            this.activeView =1
        }
    }

}
</script>

<style >
#app{
  display: grid;
  justify-content: center;
  background-color: gray;
}
</style>
