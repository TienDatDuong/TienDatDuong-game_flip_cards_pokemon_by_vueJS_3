<script setup>
import {defineEmits} from 'vue'

const  emit = defineEmits([''])
const setDefault = () => {
  emit('setDefaultAllValue')
}

</script>
<template>
  <div class="container">
    <h1 class="winner">Championships</h1>
  </div>
  <div class="container_btn">
    <button @click="setDefault">
      Start again
    </button>
  </div>
</template>
<style scoped>
.container{
  min-width: 100vw;
  text-align: center;
  animation: fade-in 2s ease-out;
}
@keyframes fade-in {
  0% { opacity: 0; font-weight: normal; }
  100% { opacity: 1; font-weight: bold; }
}
.winner{
  color: var(--light);
  font-size: 84px;
  font-family: inherit;
  padding: 10px 15px;
  background-color: var(--dark);
  display: block;
  opacity: 0.9;
}
.container_btn{
  min-width: 100vw;
  text-align: center;
  margin: 20px;
}
.container_btn button{
  border: none;
  padding: 10px 69px;
  border-radius: 5px;
  font-size: 24px;
  font-weight: 600;
  color: var(--light);
  background-color: var(--default);
  opacity: 0.95;
  cursor: pointer;
}
</style>