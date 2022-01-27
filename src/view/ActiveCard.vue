<template>
        <div class="activeCard">
        <h1>E WALLET</h1>
        <p>ACTIVE CARD</p>
        <div class="active">
            <!-- Here i am cllaing component -->
        <Card :cardProp="activCardProp(activeCard)"/>
        </div>
        <!-- this loop is to show all card -->
        <div class="list" v-for="(data, index) in
        created" v-bind:key="index"
        v-on:click="showCard(index)"
        > 
        <!-- Here i am cllaing component -->
        <Card :cardProp="cardList(index)"/>
        </div>
        <button  class="addcard" @click="activeViewfunction" > ADD NEW CARD</button>
        <!-- <button  class="addcard" > DELETE CARD</button> -->
        </div>
</template>

<script>
import Card from '../component/Card.vue'
export default {
    props:['created'],
    components:{
        Card,
    },
    data(){
        return{
            backgroundColor: '' ,
            activeView: '',
            activeCard : 0,
        }
    },
    methods:{
        activeViewfunction(){
            this.$emit('sendViewData',{...this.activeView} )
        },
        activCardProp(activeCard){
             this.activeCard
           // console.log(this.created[activeCard]);
            return this.created[activeCard]
        },
         cardList(index){
            return this.created[index]
        },
        showCard(index){
           // console.log(index)
            this.activeCard = index
        },
}
    

}
</script>

<style scoped>
.activeCard{
    display: grid;
    width: 414px;
    justify-content: center;
    grid-template-rows: auto;
    background-color: white; 
    border: 1px solid black;
}
.active{
    align-self: center;
    margin-bottom: 6rem;
}
h1, p{
    text-align: center;
    font-family: 'Source Sans Pro';
}

.list{
    display: grid;
    align-self: center;
    grid-template-rows: 6rem;

}
.addcard{
    align-self: center;
    height: 72PX;
    margin-top: 6rem;
    margin-bottom: 1rem;
    border-radius: 8px;
    color: white;
    font-weight: bold;
    background-color: black;
    font-family: 'PT Mono';
}
</style>