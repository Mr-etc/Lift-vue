<template>
  <div class="wrap">
    <Lift :prop="LiftData" />
    <Buttons :height="LiftData.height" :floor="TotlaFloor" @ChangeFloor="ChangeFloor($event)"/>
  </div>
</template>

<script>
import Lift from "@/components/Lift.vue";
import Buttons from "@/components/buttons.vue";

export default {
  name: "App",
  components: {
    Lift,
    Buttons,
  },
  data: () => ({
    LiftData: {
      height: 150,
      floor: 1,
      speed: 1,
      queue: [],
      goes: false,
      wait: false
    },
    TotlaFloor: 5,
  }),
  methods: {
    ChangeFloor(floor){
      this.LiftData.queue.push(floor);
        var Startfunc = goesFunc.bind(this); 
      if(!this.LiftData.goes){
        this.LiftData.goes = true;
        Startfunc();
      }else
        return;
      async function goesFunc(){
        let speed = Math.abs(this.LiftData.queue[0] - this.LiftData.floor);
        this.LiftData.speed = speed;
        this.LiftData.floor = this.LiftData.queue[0];
        await new Promise(resolve => setTimeout(resolve, (speed*1000)));
        this.LiftData.wait = !this.LiftData.wait;
        await new Promise(resolve => setTimeout(resolve, (3000)));
        this.LiftData.wait = !this.LiftData.wait;

        this.LiftData.queue.shift();
        if(this.LiftData.queue.length < 1)
        {
          this.LiftData.goes = false;
          return;
        }
        else
          Startfunc();
      }
    }
  }
};
</script>

<style lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
}
.wrap {
  display: flex;
  margin: 2px auto;
  width: 99%;
  min-height: 99vh;
  border: 1px solid;
  overflow: hidden;
  // background-color: #000;
}
</style>
