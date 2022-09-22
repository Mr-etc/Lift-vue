<template>
  <div class="lift-buttons">
    <div v-for="n in floor" :key="n" class="lift-buttons__item" :style="{height: height + 'px'}">
      <button @click="$emit('ChangeFloor', n)">Этаж {{n}}</button>
    </div>
  </div>
</template>
<script>
export default {
    name: 'buttons',
    props: ['height', 'floor']
}
</script>

<style lang="scss">
.lift-buttons {
  display: flex;
  flex-direction: column-reverse;
  &__item {
    & button {
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
}
</style>