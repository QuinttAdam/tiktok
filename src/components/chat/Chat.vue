<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';
    
    let message= ref(''); //int, string, boolean
    let allMessages= reactive({
        data:[],
    }); //array, object

    onMounted(async()=>{ 
        
      try {
        const response = await fetch('https://lab5-p379.onrender.com/api/v1/messages/');
        const data = await response.json();
        allMessages.data = data.slice(-10);
      } catch (error) {
        console.error('Error fetching messages:', error);
      };
    });
    
    //function sendMessage
    const sendMessage = async () => {
      try {
        const user= "henk"
        const newMessage = { text: message.value, user: user };
        const response = await fetch('https://lab5-p379.onrender.com/api/v1/messages/', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(newMessage),
        });
          

          
            
          // Update the data in a reactive way
          allMessages.data.push(newMessage);
         
          // Clear the input field after sending the message
          message.value = '';
        
      } catch (error) {
        console.error('Error sending message:', error);
    }
  };
    
</script>

<template>
  <div>
    <ul>
      <li v-for="m in allMessages.data" :key="m.id">
        <strong>{{ m.user }}</strong>: {{ m.text }}
      </li>
    </ul>
  </div>

  <div>
    <input v-model="message" type="text" placeholder="Type your message">
    <button @click="sendMessage">Send</button>
  </div>
</template>

<style scoped>

</style>