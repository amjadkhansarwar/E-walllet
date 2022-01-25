<template>
        <div class="activeCard">
        <h1>E WALLET</h1>
        <p>ACTIVE CARD</p>
        <div class="card"  > 
            <div class="card"  :class="getcolour(created[activeCard])"
            :style="{backgroundColor: colour}">
            <div class="towcolum" >
            <img :src="require('../assets/wifi.svg')" alt=""  class="img" >
            <img :src="getImgUrl(created[activeCard].vendor)" v-bind:alt="created[activeCard].vendor" class="img" width="40" height="40">
            </div><div class="img" :style="{backgroundColor: colour}">
            <img :src="require('../assets/chip.svg')" alt=""  class="img" width="40" height="40"></div>
            <div class="cardnum" ><h3>{{created[activeCard].cardnumber}}</h3></div>
            <div class="towcolum">
            <p> CARDHOLDER NAME </p>
            <p> VALID THRU </p>
            </div>
            <div class="towcolum">
            <p> {{created[activeCard].name}} </p>
            <p>{{created[activeCard].month}}/{{created[activeCard].year}}</p>
            </div>
            <li>{{created[activeCard].vendor}}</li>
            </div>
        </div>

        <div class="card" v-for="(data, index) in
        created" v-bind:key="index"
        v-on:click="showCard(index)"
        > 
        <div class="card" :class="getcolour(data)"
        :style="{backgroundColor: colour}">
        <div class="towcolum" >
        <img :src="require('../assets/wifi.svg')" alt=""  class="img" >
        <img :src="getImgUrl(data.vendor)" v-bind:alt="data.vendor" class="img" width="40" height="40">
        </div><div class="img" :style="{backgroundColor: colour}">
        <img :src="require('../assets/chip.svg')" alt=""  class="img" width="40" height="40"></div>
        <div class="cardnum" ><h3>{{data.cardnumber}}</h3></div>
        <div class="towcolum">
        <p> CARDHOLDER NAME </p>
        <p> VALID THRU </p>
        </div>
        <div class="towcolum">
        <p> {{data.name}} </p>
        <p>{{data.month}}/{{data.year}}</p>
        </div>
        </div>
        </div>
        <button  class="addcard" @click="activetab" > ADD NEW CARD</button>
        </div>
</template>

<script>
export default {
    
    props:['created'],
    
    data(){
        return{
            backgroundColor: '' ,
            activeTab: '',
            activeCard : 2,
        }
    },
    computed:{
        colour: function () {
         return this.backgroundColor
         }
    },
    methods:{
        activetab(){
            this.$emit('sendtab',{...this.activeTab} )
        },
        showCard(index){
            console.log(index)
            this.activeCard = index
        },
        getcolour(img){
                if(img.vendor == 'bitcoin'){
                 return this.backgroundColor = "#ffb74a"
                }
                if(img.vendor =='ninja'){
                 return this.backgroundColor = "#3a3a3a"
                }
                if(img.vendor ==="blockchain"){
                 return this.backgroundColor ="#7D4FE0"
                }
                if(img.vendor ==="evil"){
                 return this.backgroundColor = "#d72d4b"
                }
                return this.backgroundColor
        },
       getImgUrl(img) {
        var images = require.context('../assets/', false, /\.svg$/)
        return images('./' + img + ".svg")
        }
}
    

}
</script>

<style>
.activeCard{
    display: flex;
    flex-direction: column;
    border: 1px solid black;
    width: 420px
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
    display: block;
    align-self: center;
    border-radius: 8px;
    width: 95%;
    height: 250px;
    margin-left: 10px;
    margin-bottom: 35px;
    transform: translateY()
}
:nth-child(6)  { transform: translateY(-12rem) }
:nth-child(7)  { transform: translateY(-24rem) }
:nth-child(8)  { transform: translateY(-20rem) } 
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
.addcard{
    width: 382px;
    align-self: center;
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