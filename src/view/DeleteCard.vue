<template>
        <div class="activeCard">
        <h1>E WALLET</h1>
        <p>CLICK ON CARD THAT YOU WANT TO DELETE</p>
        
        <!-- this loop is to show all card -->
        <div class="list" v-for="(data, index) in
        created" v-bind:key="index"
        v-on:click="deletecard(index)"
        > 
        <!-- Here i am cllaing component -->
        <Card :cardProp="cardList(index)"/>
        </div>
        <button class="addbutton" @click="activeAddcardView" > ADD NEW CARD</button>
        <button class="deletebutton"  @click="activecardView" > SHOW ACTIV CARD</button> 
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
        }
    },
    methods:{
        activeAddcardView(){
            this.activeView = 2
            this.$emit('sendViewData',this.activeView )
        },
        activecardView(){
            this.activeView = 1
            this.$emit('sendViewData',this.activeView )
        },
         cardList(index){
            return this.created[index]
        },
        deletecard(index){
            let deletecard = this.created[index]
            let confirmAction = confirm("Are you sure to Delete this Card?");
            if (confirmAction) {
            this.$emit('delete', deletecard )
            alert("Card is successfully Deleted");
            } else {
            alert("Card is not deleted");
            }
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
/* .active{
    align-self: center;
    margin-bottom: 6rem;
} */
h1, p{
    text-align: center;
    font-family: 'Source Sans Pro';
}

.list{
    display: grid;
    align-self: center;
    margin-top: 6rem;
    grid-template-rows: 6rem;

}
.addbutton{
    align-self: center;
    height: 72PX;
    margin-top: 6rem;
    border-radius: 8px;
    color: white;
    font-weight: bold;
    background-color: black;
    font-family: 'PT Mono';
}
.deletebutton{
    align-self: center;
    height: 72PX;
    border-radius: 8px;
    color: white;
    font-weight: bold;
    background-color: black;
    font-family: 'PT Mono';
    margin-bottom: 1rem;
    margin-top: 00.50rem;
}
</style>