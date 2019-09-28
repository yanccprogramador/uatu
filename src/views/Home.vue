<template>
  <div class="home">
    <header class="row" >
      <div class="col s2">
        <img style="width:42%" class="responsive-img circle" src="../../public/img/uatu.jpg">
      </div>
      <div class="col s10">
        <h4>Uatu</h4>
      </div>
    </header>
    <main>
      <div class="row" v-for="conversation in conversations" v-bind:key="conversation.id">
        <div class="col s12">
        <div class="sended" v-if="conversation.type=='send'">
            {{conversation.message}}
        </div>
        <div class="received" v-else>
          {{conversation.message}}
        </div>
      </div>
      </div>
    </main> 
    <footer >
      <div class="row">
      <div class="col s11">   
      <textarea class="materialize-textarea" v-model="message">
      </textarea>
      </div>
      <div class="col s1">
      <button class="send" @click="submit"><i class="material-icons">send</i></button>
      </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
        message:'',
        conversations:[]
    }
  },
  methods:{
    submit(){
    this.conversations.push({type:'send',message:this.message})
      fetch('https://chatbot-uatu.herokuapp.com/api/message',{
        method:'POST',
        body:JSON.stringify({
          message:this.message
        })
      }).then((data)=>data.json()).then((data)=>{
        this.conversations.push({type:'receive',message:data.messageResponse})
        })
    }
  }
}
</script>
<style scoped>
body {
    display: flex;
    min-height: 100vh;
    flex-direction: column;
  }

  main {
    flex: 1 0 auto;
  }
 main{
   top:100px;
   position: fixed;
   background-image: url('../../public/img/bg.png');
   background-size: cover;
   width: 100%;
   height: 83vh;
   overflow-x: hidden;
   overflow-y: scroll;
 }
 footer{
   height: 50px;
   padding-left: 20px;
   position: fixed;
   bottom: 0;
   width: 100%;
    background-color:#275287;
   color: #E4E947
 }
 footer textarea{
   color: #fff;
 }
 header{
   position: fixed;
   top: 0;
   width: 100%;
   margin: 0;
   background-color:#275287;
   color: #E4E947;
   margin:0!important;
   height:100px
 }
 .send{
   background-color: unset;
border: unset;
margin-top: 15px;
color: #E4E947;
 }
 .sended{
   background-color: #7599C6;
   float: right;
   margin: 50px;
   padding: 20px;
margin: 20px;
color: #fff
 }
 .received{
   background-color: #FFFF63;
   float: left;
   margin: 50px;
   padding: 20px;
margin: 20px;
 }
</style>