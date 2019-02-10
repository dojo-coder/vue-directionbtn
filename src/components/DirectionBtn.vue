<template>
    <div class="btn" @mouseenter="onMouseEnter" @mouseleave="onMouseLeave">
        <div ref="before" class="before"></div>
        <a ref="txt">{{opts}}</a>
    </div>
</template>

<script>
import {TweenMax, TimelineMax} from 'gsap'
export default {
  props: {
    opts: String
  },
  name: 'DirectionBtn',
  data(){
    return {
      anim:{
        isPlaying: false,
        startX: '0%',
        midX: '50%',
        startY: '100%',
        stopX: '0%',
        midY: '50%',
        stopY: '0%',
        duration: 0.3
      }
    }
  },
  methods: {
    animLeave(e){
      let direction;
      let classnametarget = e.target.className.replace('line','').trim();
      
      let elWidth = this.$el.offsetWidth;
      let elHeight = this.$el.offsetHeight;

      let dists = {
        distLeft: e.offsetX, 
        distRight: elWidth - e.offsetX, 
        distTop: e.offsetY, 
        distBottom: elHeight - e.offsetY
      };

      let min = Math.min(dists.distLeft, dists.distRight, dists.distTop, dists.distBottom);
      console.log(min)
      switch(min){
        case dists.distTop:
          direction = 2;
          break;
        case dists.distRight:
          direction =  3;
          break;
        case dists.distBottom:
          direction = 0;
          break;
        case dists.distLeft:
          direction = 1;
          break;
          
         
      }
      
      this.setAnimPos(direction);
       TweenMax.to(this.$refs.before, this.anim.duration,
       {
         x: this.anim.stopX,
         y: this.anim.stopY,
         onComplete: this.setPlay.bind(this)
       });
      this.tlMouseHover = false;
      this.$refs.txt.style.color = "";
    },
    onMouseLeave: function(e){
      if(this.tlMouseHover){
        this.tlMouseHover.eventCallback("onComplete", this.animLeave.bind(this), [e]);

      }
      else
        this.animLeave(e);
      
    },
    onMouseEnter: function(e){
      console.log(e, 'onMouseEnter');
      if(this.anim.isPlaying)
        return false;
      console.log(this);
      // let direction = this.getDirection(e, this.$el);
      let direction;
      let classnametarget = e.target.className.replace('line','').trim();
      
      let elWidth = this.$el.offsetWidth;
      let elHeight = this.$el.offsetHeight;

      let dists = {
        distLeft: event.offsetX, 
        distRight: elWidth - e.offsetX, 
        distTop: e.offsetY, 
        distBottom: elHeight - e.offsetY
      };

      let min = Math.min(dists.distLeft, dists.distRight, dists.distTop, dists.distBottom);
      console.log(min)
      switch(min){
        case dists.distTop:
          direction = 0;
          break;
        case dists.distRight:
          direction =  1;
          break;
        case dists.distBottom:
          direction = 2;
          break;
        case dists.distLeft:
          direction = 3;
          break;
          
         
      }
      this.setAnimPos(direction);
      console.log('direction:', classnametarget, direction,this.anim);
      console.log(this.$refs.before);
      
    
      this.anim.isPlaying = true;
      this.tlMouseHover  = new TimelineMax({
        onComplete: () => { 
          this.tlMouseHover = false;
        }
      });
      this.tlMouseHover.fromTo(this.$refs.before, this.anim.duration, {
        x: this.anim.startX,
        y: this.anim.startY,
      },{
        x: this.anim.midX,
        y: this.anim.midY
      })
      this.$refs.txt.style.color = "white";
      // tl.fromTo(this.$refs.before, 1, {
      //   x: this.anim.startX,
      //   y: this.anim.startY,
      // },{
      //   x: this.anim.stopX,
      //   y: this.anim.stopY,
      // });
    },
    setPlay: function(){
       this.anim.isPlaying = false;
      // this.btns = true;
    },
    setAnimPos: function(dir){
      let oRes = this.anim;
       switch(dir){
         case 0:
           oRes.startX = '0%';
           oRes.startY = '-100%';
           oRes.midX = "0%";
           oRes.midY = "0%";
           oRes.stopX = '0%';
           oRes.stopY = '101%';
           break;
         case 1:
           oRes.startX = '100%';
           oRes.startY = '0%';
           oRes.midX = "0%";
           oRes.midY = "0%";
           oRes.stopX = '-101%';
           oRes.stopY = '0%';
           break;
         case 2:
           oRes.startX= '0%';
           oRes.startY='100%';
           oRes.midX = "0%";
           oRes.midY = "0%";
           oRes.stopX = '0%';
           oRes.stopY = '-101%'
           break;
         case 3:
           oRes.startX= '-100%';
           oRes.startY= '0%'; 
           oRes.midX = "0%";
           oRes.midY = "0%";
           oRes.stopX = '101%';
           oRes.stopY = '0%';
           break;
       }
    },
    
  },
  mounted(){
      let tl = new TimelineMax({
        paused: true
      });
      
      TweenMax.set(this.$refs.before,{
        x: this.anim.startX,
        y: this.anim.startY
      });
      
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
