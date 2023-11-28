<script setup>
import Chat from './components/chat/Chat.vue';
import VideoDetails from './components/video/VideoDetails.vue';
import VideoPlayer from './components/video/VideoPlayer.vue';

import { ref } from 'vue';
let newDescription = ref("default description");

const updateVideo = (description) => {
  newDescription.value = description;
};

</script>

<template>
  <div class="tiktok">
    <div>
      <VideoPlayer @update:video-description="updateVideo"/>
    </div>
    <div>
      <VideoDetails :description="newDescription"/>
      <Chat />
    </div>
  </div>
</template>

<style scoped>
  .tiktok {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
</style>