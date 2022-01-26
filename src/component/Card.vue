<template>
  <div class="container" id="card" :class="cardProp.vendor">
      <img class="image1" :src="require('../assets/wifi.svg')" alt="" >
      <img class="image2"   id="img" width="40" height="40">
      <img class="image3" :src="require('../assets/chip.svg')" alt=""   width="40" height="40">
      <h3 class="cardNumber">{{cardProp.cardnumber}}</h3>
      <p> CARDHOLDER NAME </p>
      <p> VALID THRU </p>
      <p>{{cardProp.name}}</p>
      <p>{{cardProp.month}}/{{cardProp.year}}</p>
  </div>
</template>

<script>
export default {
    props:[
        'cardProp'
        ],
        data(){
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
}
</script>

<style scoped >
.container{
    display: grid;
    border-radius: 8px;
    width: 382px;
    height: 250px;
    margin-bottom: 1rem;
    grid-template-columns: 180px 180px;
    grid-template-rows: auto;
    background-color: #D0D0D0;
    justify-items: center;
    padding-top: 0.50rem;
    align-self: center;
}
.image1, .image3 {
    padding-left: 1rem;
    justify-self: start;
}
.image2{
    justify-self: end;
    content:url('../assets/bitcoin-logo.png');
}
.cardNumber{
 grid-column-start: 1;
  grid-column-end: 3;
}
.Bitcoin{
    background-color: #ffb74a;
}
.Evil{
    background-color: #d72d4b;
}
.Ninja{
    background-color: #3a3a3a;
}
.Blockchain{
    background-color: #7D4FE0;
}
.Evil .image2{
    content:url("../assets/Evil.svg");
}
.Ninja .image2{
    content:url("../assets/Ninja.svg");
}
.Bitcoin .image2{
    content:url("../assets/Bitcoin.svg");
}
.Blockchain .image2{
    content:url("../assets/Blockchain.svg");
}
</style>