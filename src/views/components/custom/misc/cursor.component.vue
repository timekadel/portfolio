<template>
  <div class="wrapper">
    <div ref="cursor" class="cursor"/>
    <div ref="pointer" class="pointer"/>
    <div ref="floaters" class="floaters">

    </div>

  </div>
</template>

<script>
export default {
  name: "CursorComponent",
  mounted(){
    window.addEventListener('mousemove', this.handleCursorMovement);
    window.addEventListener('mousedown', this.handleMouseDown);
    window.addEventListener('mouseup', this.handleMouseUp);
    document.body.style.cursor = 'none';
  },
  methods:{
    handleCursorMovement(e){
      const cursorEl = this.$refs.cursor;
      const pointerEl = this.$refs.pointer;
      const {clientX: x, clientY: y} = e;
      cursorEl.style.top = y - 30 + "px";
      cursorEl.style.left = x - 30 + "px";
      pointerEl.style.top = y - 10 + "px";
      pointerEl.style.left = x - 10 + "px";
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
  position: absolute;
  height: 60px;
  width: 60px;
  background: #ffffffe0;
  border-radius: 50%;
  mix-blend-mode:difference;
  transition: all .1s ease-out;
  pointer-events: none;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: scale(1);
}
.pointer{
  position: absolute;
  height: 20px;
  width: 20px;
  background: #ffffff30;
  mix-blend-mode:difference;
  border-radius: 50%;
  transition: all .07s;
}
.cursor.clicked{
  transform: scale(.9);
}
</style>