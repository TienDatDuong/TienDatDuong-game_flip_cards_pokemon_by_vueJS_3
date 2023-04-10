<template>
  <div>
    <MainScreen v-if="type === 'default'" @getStart="getStart" @getTotalOfBlock="getNumberArray" />
    <InteractScreen v-if="type === 'match'" :cardsContext="setting.cardsContext" @getWinner='getWinner'/>
    <ResultSrceen v-if="type === 'winnner'" @setDefaultAllValue="setDefaultAllValue" />
    <CopyRightScreent/>
  </div>

</template>

<script setup>
import MainScreen from "@/components/mainScreen";
import InteractScreen from './components/InteractScreen'
import CopyRightScreent from "@/components/copyRightScreent";
import ResultSrceen from "@/components/resultSrceen";
import {reactive, ref} from "vue";
import {shuffle} from "@/ultils/customUtils";

const type = ref('default')
const array = ref([])
const array2 = ref([])
const cards = ref([])

const setting = reactive({configGame: 0, cardsContext:[]})

const getStart = () =>{
  if(setting.cardsContext.length > 1){
  type.value = 'match'
  }else {
    alert('please choose level do you want play game !')
  }
}
const getWinner = () => {
  type.value = 'winnner'
}

const setDefaultAllValue = () => {
  type.value = 'default'
  setting.cardsContext = []
}

const getNumberArray = (config) => {
  setting.configGame = config
  array.value = Array.from({length: Number(config.totalOfBlock)/ 2}, (_, i) => i + 1)
  array2.value = [...array.value]
  cards.value = [...array2.value, ...array.value]
  setting.cardsContext = shuffle(cards.value)
}


</script>

<style>

</style>
