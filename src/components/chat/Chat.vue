<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';
    
    let message= ref(''); //int, string, boolean
    let allMessages= reactive({
        data:["heel", "even", "simpel", "doen"],
    }); //array, object

    //function sendMessage
    const sendMessage=()=>{
        allMessages.data.push(message.value);
        message.value = '';
    }
</script>

<template>
  <div>
    <ul>
        <li v-for="m in allMessages.data">{{ m }}</li>
    </ul>
  </div>

  <div>
    <input v-model="message" type="text" placeholder="">
    <button @click="sendMessage">Send</button>
  </div>
</template>

<style scoped>

</style>