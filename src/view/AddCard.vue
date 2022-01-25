<template>
<div class="addCard">
    <h1>ADD A NEW BANK CARD</h1>
    <p>NEW CARD</p>
    <div class="card" :style="{backgroundColor: colour}">
         <div class="towcolum">
        <img :src="require('../assets/wifi.svg')" alt=""  class="img" >
        <img :src="getImgUrl(card.vendor)" alt="" class="img" width="40" height="40">
        </div><div class="img" >
        <img :src="require('../assets/chip.svg')" alt=""  class="img" width="40" height="40"></div>
        <div class="cardnum"><h3>{{card.cardnumber}}</h3></div>
        <div class="towcolum">
         <p> CARDHOLDER NAME </p>
        <p> VALID THRU </p>
        </div>
        <div class="towcolum">
         <p>{{card.name}}</p>
        <p>{{card.month}}/{{card.year}}</p>
        </div>
    </div>
    <form @submit.prevent="submit">
        <label> CARD NUMBER</label>
        <input type="text" placeholder="Card Number" v-model="card.cardnumber" required>
        <label> CARDHOLDER NAME</label>
        <input type="text" placeholder="FRISTNAME LASTNAME" v-model="card.name" required>
        <div class="date">
        <label class="halfrow"> MONTH</label>
        <label class="halfrow"> YEAR</label>
        <select v-model="card.month"  class="halfrow" required>
        <option v-for="(month,index) in monthname" :key="index" >
            {{month}}</option>
        </select>
        <select v-model="card.year" class="halfrow"  required>
        <option v-for="(year,index) in yearname" :key="index" >
            {{year}}</option>
        </select>
        </div>
        <label> VENDOR</label>
        <select v-model="card.vendor" required>
        <option v-for="(vendor,index) in vendorname" :key="index" >
            {{vendor}}</option>
        </select>
        <button> ADD CARD</button>
    </form>
</div>
</template>

<script>
export default {
    data(){
        return{
            card:
            {
                cardnumber:'',
                name:'',
                month:'',
                year: '',
                vendor: 'e'
            },
            vendorname:
            ['bitcoin','ninja','blockchain','evil'],
            monthname:
            ['01','02','03','04','05','06','07','08','09','10','11','12'],
            yearname:
            ['22','23','24','25'],
        
            backgroundColor: ''
            
      }
    
    },
    computed:{
        colour: function () {
         return this.backgroundColor
         }
    },
    methods:{
        submit(){
            this.$emit('send',{...this.card} )
        },
        getImgUrl(img) {
        if(img ==="bitcoin"){
        this.backgroundColor = "#ffb74a"
        }if (img ==="ninja") {
        this.backgroundColor = "#3a3a3a"
        } if (img ==="blockchain") {
        this.backgroundColor = "#7D4FE0"   
        } if(img ==="evil"){
        this.backgroundColor = "#d72d4b"
        }
        var images = require.context('../assets/', false, /\.svg$/)
        return images('./' + img + ".svg")
        }
    }

}
</script>

<style scoped>
.addCard{
    display: flex;
    flex-direction: column;
    border: 1px solid black;
    width: 420px;
}
h1, p{
    display: flex;
    width: 250px;
    justify-content: center;
    align-self: center;
    margin: 12px;
    font-family: 'Source Sans Pro';
}
.card{
    display: flex;
    flex-direction: column;
    border-radius: 8px;
    width: 382px;
    height: 250px;
    align-self: center;
    background-color: #D0D0D0;
    margin-bottom: 35px;
    color: white;
}
.towcolum{
    display: flex;
    justify-content: space-between;
    margin-top: 6px;
    margin-right: 10px;
}
.img{
    margin-left: 6px;
}
.cardnum{
    display: flex;
    justify-content: center; 
}
form{
    display: flex;
    flex-direction: column;
    width: 382px;
    align-self: center;
   
}
.date{
    display: flex;
    flex-wrap: wrap;
    column-gap: 30px;
    font-family: 'PT Mono';
}
.halfrow{
    flex: 44%;
}
input, select{
    height: 56px;
    border-radius: 8px;
    margin-bottom: 12px;
    border: 1px solid black;
    font-family: 'PT Mono';
}
button{
    height: 72PX;
    margin-top: 24px;
    margin-bottom: 12px;
    border-radius: 8px;
    color: white;
    font-weight: bold;
    background-color: black;
    font-family: 'PT Mono';
}
</style>