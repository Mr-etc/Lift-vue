<template>
  <div class="lift-body">
    <!-- <div  class="lift-item"></div> -->
    <div
      :style="{
        height: height + 'px',
        bottom: (prop.floor - 1) * height + 'px',
        'transition-duration': prop.speed + 's',
      }"
      class="lift-item"
      :class="{ 'lift-item_wait': prop.wait }"
    >
      <span v-show="prop.goes">{{prop.floor}} этаж</span>
    </div>
  </div>
</template>
<script>
export default {
  name: "lift",
  props: ["prop", 'height'],
};
</script>
<style lang="scss">
.lift {
  &-body {
    position: relative;
    width: 100px;
    margin: 0 10px;
    border: 1px solid silver;
  }
  &-item {
    position: absolute;
    bottom: 0;
    width: 100%;
    background-color: aqua;
    transition: bottom 1s linear;
    & span {
      display: table;
      padding: 10px;
      margin: 5px auto;
      background-color: rgba(112, 128, 144, 0.603);
      border-radius: 5px;
      color: #fff;
      letter-spacing: 1px;
    }
    &_wait {
      animation: LiftWait 1s infinite linear;
    }
  }
}
@keyframes LiftWait {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.4;
  }
  100% {
    opacity: 1;
  }
}
</style>