<template>
  <div class="card" :class="{disable: isDisable}"
       :style="{
    height: `${(690 - 16 * 4)/ Math.sqrt(props.cardsContext?.length)-16}px`,
  width: `${(((690 - 16 * 4)/ Math.sqrt(props.cardsContext?.length)-16)*3)/4}px`}">
    <div class="flip-card-inner" :class="{'is-covered' : isChangeCard}" @click="getChangeCard">
      <div class="flip-card-front">
        <div class="flip-card-front-content"
             :style="{backgroundSize: `${((((690 - 16 * 4)/ Math.sqrt(props.cardsContext?.length)-16)*3)/4)/2}px`}"/>
      </div>
      <div class="flip-card-back">
        <img :src="require(`@/assets/pokemonImage/${props?.img}`)"
             :style="{backgroundSize: `${((((690 - 16 * 4)/ Math.sqrt(props.cardsContext?.length)-16)*3)/4)/2}px`}"/>
      </div>
    </div>
  </div>
</template>
<script setup>
import {ref, defineProps, defineEmits, defineExpose} from "vue";

const emit = defineEmits(['selectedCard'])

const props = defineProps({
  setCards: Function,
  card: {
    type: [String, Number, Array, Object],
  },
  img: {
    type: String,
    required: true,
    default: ''
  },
  cardsContext: {
    type: Array,
    required: true,
    default: () => {
    }
  }
})
const isDisable = ref(false)
const isChangeCard = ref(false)
const getChangeCard = () => {
  if (isDisable.value) return false
  isChangeCard.value = !isChangeCard.value
  if (isChangeCard.value) {
    emit('selectedCard', props.card)
  }
}
console.log('props.cardsContext',props)
const onEnabledDisableMode = () => {
  isDisable.value = true
}
const setCards = () => {
  setTimeout(() => {
    isChangeCard.value = false
  }, 300)

}
defineExpose({
  setCards,
  onEnabledDisableMode
});
</script>
<style scoped>
.card {
  display: inline-block;
  margin-bottom: 1rem;
  margin-right: 1rem;
  perspective: 200px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  cursor: pointer;
}

.card.disable .flip-card-inner {
  cursor: default;
}

.flip-card-inner.is-covered {
  transform: rotatey(180deg);
}

.flip-card-inner.is-uncovered {
  pointer-events: none;
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: var(--dark);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
}

.flip-card-back {
  background-color: #dcfbf3;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: rotateY(180deg);
  border-radius: 5px;
}

.flip-card-front .flip-card-front-content {
  background: url("@/assets/pokemonImage/icon_back.png") no-repeat center center;
  height: 100%;
  width: 100%;
}

img {
  width: 50px;
  height: 70px;
}
</style>