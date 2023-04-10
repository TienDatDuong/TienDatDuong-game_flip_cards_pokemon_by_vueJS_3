<template>
  <div class="contaier">
    <div class="contaier_inner" :style="{width: `${
      ((((690 - 16 * 4)/ Math.sqrt(props.cardsContext?.length) -16)* 3)/4 + 16)* Math.sqrt(props.cardsContext?.length)
    }px` }">
      <cardsComponent :ref="`helloWorldRef`" :cardsContext="props.cardsContext" class="contaier-cards"
                      v-for="(item,idx) in props.cardsContext" :key="idx" :img="`${item}.png`"
                      :card="{index:idx,value:item}" @selectedCard="selectedCard"/>
    </div>
  </div>
</template>
<script setup>
import CardsComponent from "@/components/CardsComponent.vue";
import {ref, defineProps, defineEmits} from 'vue'

const emit = defineEmits(['getWinner'])

const props = defineProps({
  cardsContext: {
    type: Array,
    required: true,
    default: () => {
    }
  }
})


const helloWorldRef = ref([])
const rules = ref([])


const selectedCard = (item) => {
  if (rules.value.length === 2) return false
  rules.value.push(item)
  if (rules.value.length === 2 && rules.value[0].value === rules.value[1].value) {
    const index1 = rules.value[1].index
    const index0 = rules.value[0].index
    helloWorldRef.value[index1].onEnabledDisableMode()
    helloWorldRef.value[index0].onEnabledDisableMode()
    const countDisabled = document.querySelectorAll('.contaier .card.disable')
    rules.value = []
    if (countDisabled && countDisabled.length === props.cardsContext.length - 2) {
      setTimeout(() => {
        emit('getWinner')
      }, 920)
    }
  } else if (rules.value.length === 2 && rules.value[0].value !== rules.value[1].value) {
    const index1 = rules.value[1].index
    const index0 = rules.value[0].index
    helloWorldRef.value[index1].setCards()
    helloWorldRef.value[index0].setCards()
    rules.value = []
  } else {
    return false
  }
}
</script>
<style scoped>
.contaier {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}

.contaier_inner {
  margin: 2rem auto;
  display: flex;
  flex-wrap: wrap;
}

.contaier-cards {
  display: inline-block;
}
</style>