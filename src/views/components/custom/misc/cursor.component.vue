<template>
  <div class="wrapper">
    <div ref="cursor" class="cursor"/>
    <div ref="pointer" class="pointer"/>
    <div ref="floaters" class="floaters">

    </div>

  </div>
</template>

<script>
import _ from 'lodash'
console.log(_)
export default {
  name: "CursorComponent",
  mounted(){
    window.addEventListener('mousemove', this.handleCursorMovement);
    window.addEventListener('mousedown', this.handleMouseDown);
    window.addEventListener('mouseup', this.handleMouseUp);
    // window.addEventListener('touchmove', this.diasbleCursorVisibilityPermanently);
    document.body.style.cursor = 'none';
  },
  data:()=>({
    timerHandle: null  
  }),
  methods:{
    handleCursorMovement(e){
      const cursorEl = this.$refs.cursor;
      const pointerEl = this.$refs.pointer;
      if(cursorEl && pointerEl){
      clearTimeout(this.timerHandle)
      const {clientX: x, clientY: y} = e;
      cursorEl.style.opacity = 1;
      pointerEl.style.opacity = 1;
      cursorEl.style.transform = `translate(${x - 30}px,${y - 30}px)`
      pointerEl.style.transform = `translate(${x - 10}px,${y - 10}px)`
      this.timerHandle = setTimeout(this.diasbleCursorVisibility,2000);
      console.log("ok")
      }
    },
    diasbleCursorVisibilityPermanently(){
      const cursorEl = this.$refs.cursor;
      const pointerEl = this.$refs.pointer;
      cursorEl.style.display = "none";
      pointerEl.style.display = "none";
    },
    diasbleCursorVisibility(){
      const cursorEl = this.$refs.cursor;
      const pointerEl = this.$refs.pointer;
      cursorEl.style.opacity = 0;
      pointerEl.style.opacity = 0;
    },
    handleMouseDown(){
      const cursorEl = this.$refs.cursor;
      cursorEl.classList.add('clicked')
    },
    handleMouseUp(){
      const cursorEl = this.$refs.cursor;
      cursorEl.classList.remove('clicked')
    },
  },
}
</script>

<style>
input, textarea,.cursor-pointer,.cursor-hand{
  cursor: none!important;
}
</style>

<style scoped>
.wrapper{
  position: fixed;
  height: 100vh;
  width: 100vwx;
  top:0;
  left:0;
  pointer-events: none;
  mix-blend-mode:difference;
  z-index:999;
}
.cursor{
  opacity: 0;
  position: absolute;
  height: 60px;
  width: 60px;
  background: #ffffffe0;
  border-radius: 50%;
  mix-blend-mode:difference;
  pointer-events: none;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: scale(1);
  transition: transform .1s ease-out, opacity .1s ease-in-out;
}
.pointer{
  opacity: 0;
  position: absolute;
  height: 20px;
  width: 20px;
  background: #ffffff30;
  mix-blend-mode:difference;
  border-radius: 50%;
  transition: transform .06s ease-out, opacity .1s ease-in-out;
}
.cursor.clicked{
  transform: scale(.9);
}
</style>