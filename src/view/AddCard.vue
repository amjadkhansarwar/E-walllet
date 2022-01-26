<template>
<div class="addCard" id="App">
    <h1>ADD A NEW BANK CARD</h1>
    <p>NEW CARD</p>
    <div class="card">
        <!-- this is child  -->
     <Card :cardProp="cardProp"/>
    </div>
    <form @submit.prevent="submit">
        <div class="container">
        <span>  CARD NUMBER</span>
        <input type="number" placeholder=" XXXX-XXXX-XXXX-XXXX " 
         v-model.number="card.cardnumber"
          required>
        <span> CARDHOLDER NAME</span>
        <input type="text" onkeypress="return /[a-z]/i.test(event.key)" 
        placeholder="FRISTNAME  LASTNAME"
        v-model="card.name" 
        required>
        <span> MONTH</span>
        <label> YEAR</label>
        <select v-model="card.month"  class="halfrow" required>
        <option v-for="(month,index) in monthname" :key="index" >
         {{month}}
         </option>
        </select>
        <select v-model="card.year" class="halfrow"  required>
        <option v-for="(year,index) in yearname" :key="index" >
        {{year}}
        </option>
        </select>
        <span>VENDOR</span>
        <select class ="select" v-model="card.vendor" required>
        <option v-for="(vendor,index) in vendorname" :key="index" >
        {{vendor}}
        </option>
        </select>
        <button> ADD CARD</button>
        </div>
    </form>
</div>
</template>

<script>
import Card from '../component/Card'
export default {
    components:{
        Card,
    },
    data(){
        return{
            card:
            {
                cardnumber:'',
                name:'',
                month:'',
                year: '',
                vendor: '',
            },
            vendorname:
            ['bitcoin','ninja','blockchain','evil'],
            monthname:
            ['01','02','03','04','05','06','07','08','09','10','11','12'],
            yearname:
            ['22','23','24','25'],
      }
    
    },
    computed:{
        cardProp(){
            return this.card
        },
    },
    methods:{
        submit(){
            let validcard =this.card.cardnumber
            validcard = validcard.toString().length
            if(validcard < 16 || validcard > 16 ){
            alert('You just put '+ validcard +' digits. Please add 16 digits')
            return
            }
            this.$emit('send',{...this.card} )
        },
    }


}
</script>

<style scoped>
.addCard{
    display: grid;
    width: 33rem;
    justify-content: center;
    grid-template-rows: auto;
    background-color: white; 
    border: 1px solid black;
}
h1, p{
    text-align: center;
    font-family: 'Source Sans Pro';
}
.card{
    display: grid;
    align-self: center;
}

.container{
    display: grid;
    grid-template-columns: 173px 173px;
    grid-template-rows: auto;
    column-gap: 36px;
}
label{
    grid-column-start: 2;
    grid-column-end: 3;
}
input, .select, button{
    grid-column-start: 1;
    grid-column-end: 3;
 }
 input, select, button{
                height: 3.33rem;
                border-radius: 8px;
                margin-bottom: 12px;
                border: 1px solid black;
                font-weight: bold;
                font-family: 'PT Mono'; 
}
 button{
        color: white;
        background-color: black;
} 
</style>