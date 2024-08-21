<template>
  <transition name="fade">
    <div v-if="isPromptVisible" class="prompt-bar">
      <span class="key">{{ message }}</span>
    </div>
  </transition>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import { useEvents } from '@Composables/useEvents.js';

const isPromptVisible = ref(false);
const message = ref('按E打开ATM');
const events = useEvents();

events.on('showpromptbar', (message1: string) => {
  isPromptVisible.value = true;
  message.value = message1;
});

events.on('hidepromptbar', () => {
  isPromptVisible.value = false;
});
</script>

<style scoped>
.prompt-bar {
  position: fixed;
  bottom: 33vh;
  right: 33vw;
  background: rgba(255, 255, 255, 0.1); 
  border: 1px solid rgba(255, 255, 255, 0.3); 
  border-radius: 8px; 
  padding: 10px 20px; 
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5); 
}

.key {
  color: #ffffff;
  font-size: 18px; 
  font-weight: 600;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.8); 
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>
