<template>
  <div class="about">
    <textarea v-model="message">
    </textarea>
    <button @click="submit">Enviar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
        message:''
    }
  },
  methods:{
    submit(){
      fetch('https://chatbot-uatu.herokuapp.com/api/message',{
        method:'POST',
        body:JSON.stringify({
          message:this.message
        })
      }).then((data)=>data.json()).then((data)=>alert(data.message))
    }
  }
}
</script>
