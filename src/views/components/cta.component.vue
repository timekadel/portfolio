<template>
  <div
    @click="$emit('pressed')"
    :class="{ light, filled }"
    class="btn font-medium cursor-pointer uppercase flex items-center justify-center bottom-5 right-5 rounded-full h-12 md:pl-8 md:pr-8 flex-1 lg:flex-none"
  >
    <span class="text">{{ title }}</span>
    <eva-icon v-if="filled" class="icon" name="arrow-right" :fill="light ? '#e7e7e7':'#222020'"></eva-icon>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    filled: {
      type: Boolean,
      default: false,
    },
    light: {
      type: Boolean,
      default: false,
    },
  },
  name: "CTAComponent",
};
</script>

<style scoped>
.btn {
  border: 2px solid #e7e7e7;
  color: #e7e7e7;
  transition: all ease-in-out .25s;
  border-radius: 50px;
}
.btn.light {
  border-color: #222020;
  color: #222020;
}
.btn.light.filled {
  background: #222020;
  color: #e7e7e7;
}
.btn.filled {
  background: #e7e7e7;
  color: #222020;
  border-color: transparent;
}
.btn:hover {
  opacity: 1!important;
}
.btn.filled:hover > .text{
  transform: translateX(-8px);
}

.text{
  transform: translateX(0px);
  height: 100%;
  display: flex;
  align-items: center;
  transition: all .1s;
  font-weight: 600;
}
.icon{
  width: 0px;
  opacity: 0;
  transition: all .1s;
}
.btn:hover > .icon{
 opacity: 1;
 margin-left:-8px;
 margin-right: 8px;
}
</style>
