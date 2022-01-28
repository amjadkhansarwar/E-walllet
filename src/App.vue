
<template>
 <!-- here i am calling my views -->
<div id="app" class="app">
  <ActiveCard v-if="activeView === 1" :created="created" @sendViewData="viewData"/>
  <DeleteCard v-if="activeView === 3"  :created="created" @sendViewData="viewData"
  @delete="deletecard"/>
  <AddCard    v-if="activeView === 2"  @send="addcard"/>
</div>
</template>

<script>
import AddCard from './view/AddCard'
import ActiveCard from './view/ActiveCard'
import DeleteCard from './view/DeleteCard'
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
        DeleteCard
        },
      data(){
        //localStorage.removeItem("cardData");
        return{
          activeView: 1,
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
        }
      },
      methods:{

        viewData(receivedview){
          return this.activeView = receivedview
        },
        deletecard(deltecarddata){
          let localobj = []
          localobj = getData()
          if(localobj){
          localobj = JSON.parse(localobj)
          localobj =[...localobj]
          const  result  = localobj.filter( deleteCard => deleteCard.cardnumber !=deltecarddata.cardnumber)
          this.card = result
          sendDataLocalStorage(this.card)
          }
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
                    //  Uppdate card orDeleteing duplicate card with respect to vendor
                let counter =0
                let i = 0
                for ( i = 0; i < nycount.length; i++) {
                if (nycount[i].vendor) 
                counter++;
                }
                if(counter >= 4)
                {
                alert("Your limt of cards in wallet is full now. you want to Uppdate  first one card and save this one")
                const result = nycount.filter(word => word.vendor != cardData.vendor);
                this.card = result
                sendDataLocalStorage(this.card)
                }
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
