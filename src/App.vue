<template>
  <div class="wrap">
    <Lift v-for="(lift, key) in LiftData.LiftObj" :key="key" :prop="lift" :height="LiftData.height"/>
    <!-- <Lift :prop="LiftData" /> -->
    <Buttons :height="LiftData.height" :floor="LiftData.TotlaFloor" @ChangeFloor="ChangeFloor($event)"/>
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
      queue: [],
      TotlaFloor: 5,
      LiftObj:[
        {
          floor: 1,
          speed: 1,
          goes: false,
          wait: false
        },
        {
          floor: 1,
          speed: 1,
          goes: false,
          wait: false
        }
      ],
    }
  }),
  methods: {
    ChangeFloor(floor){
      this.LiftData.queue.push(floor);
      var Startfunc = goesFunc.bind(this); 
      for(let i = 0; i<this.LiftData.LiftObj.length; i++){
        if(!this.LiftData.LiftObj[i].goes){
          this.LiftData.LiftObj[i].goes = true;
          Startfunc(i);
          return;
        }else if(i == (this.LiftData.LiftObj.length-1))
          return;
      }
      async function goesFunc(key){
        let speed = Math.abs(this.LiftData.queue[0] - this.LiftData.LiftObj[key].floor);
        this.LiftData.LiftObj[key].speed = speed;
        this.LiftData.LiftObj[key].floor = this.LiftData.queue[0];
        this.LiftData.queue.shift();
        await new Promise(resolve => setTimeout(resolve, (speed*1000)));
        this.LiftData.LiftObj[key].wait = !this.LiftData.LiftObj[key].wait;
        await new Promise(resolve => setTimeout(resolve, (3000)));
        this.LiftData.LiftObj[key].wait = !this.LiftData.LiftObj[key].wait;
        if(this.LiftData.queue.length < 1)
        {
          this.LiftData.LiftObj[key].goes = false;
          return;
        }
        else
          Startfunc(key);
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
