<template>
  <div class="container_main">
    <h1>POKEMON MEMORIES</h1>
    <P>Select mode to start game</P>
    <ul>
      <li>
        <button class="btn_select" :class="{selected : type === 16}" @click="totalOfBlock(16)">
          4x4
          <br>
          Easy
        </button>
      </li>
      <li>
        <button class="btn_select" :class="{selected : type === 36}" @click="totalOfBlock(36)">
          6x6
          <br>
          Normal
        </button>
      </li>
      <li>
        <button class="btn_select" :class="{selected : type === 64}" @click="totalOfBlock(64)">
          8x8
          <br>
          Hard
        </button>
      </li>
      <li>
        <button class="btn_select" :class="{selected : type === 100}" @click="totalOfBlock(100)">
          10x10
          <br>
          Super hard
        </button>
      </li>
    </ul>
    <button class="btn_start" @click="startGame">Start game</button>
  </div>
</template>
<script setup>
import {defineEmits, reactive, ref} from 'vue'

const emit = defineEmits(['getStart', 'getTotalOfBlock'])


const startGame = () => {
  emit('getStart')
}

const settings = reactive({totalOfBlock: 0})
const type = ref(0)

const totalOfBlock = (config) => {
  type.value = config
  settings.totalOfBlock = config
  emit('getTotalOfBlock', {totalOfBlock: settings.totalOfBlock})
}

</script>
<style scoped>
.container_main {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: var(--light);
  background-color: var(--default);
  padding: 20px;
  opacity: 0.8;
  border-radius: 5%;
  box-shadow: 5px 10px #6f2f44;
}

h1, p, ul {
  margin-bottom: 5%;
}

ul {
  display: flex;
}

li {
  list-style-type: none
}

.btn_select {
  border: none;
  min-height: 60px;
  min-width: 100px;
  margin: 10px;
  border-radius: 5px;
  background-color: var(--light);
  cursor: pointer;
  font-weight: 600;
  color: var(--default);
}

.btn_select:hover {
  background-color: var(--yellow);
}

.selected {
  background-color: var(--yellow);
  color: var(--default);
}

.btn_start {
  width: 98%;
  margin: auto;
  padding: 2%;
  font-weight: 600;
  color: var(--default);
  font-size: 24px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
}

.btn_start:hover {
  background-color: var(--green);
  color: var(--light);
}
</style>