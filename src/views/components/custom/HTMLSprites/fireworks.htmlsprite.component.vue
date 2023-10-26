<template>
  <div class="HomeHTMLSprite">
    <Transition name="fade">
      <div v-if="displayed">
        <h1 class="text-white opacity-90 z-10 text-6xl sm:text-6xl md:max-w-2xl lg:text-7xl xl:text-8xl font-bold">I Make Fireworks.</h1>
        <br />
        <h3 class="z-10 text-white text-2xl sm:text-2xl xl:text-3xl max-w-xl font-thin opacity-90">
          I'm a <b>professional pyrotechnician</b> firing large <b>pyromusical</b> shows accross <b>France and England</b> since 2012.
        </h3>
      </div>
    </Transition>
  </div>
</template>

<script>
import * as THREE from "three";
import HTMLSpriteMixin from "@/mixins/HTMLSprite.mixin.js";

export default {
  name: "FireworksHTMLSprite",
  mixins: [HTMLSpriteMixin],
  data() {
    return {
      position: new THREE.Vector3(1.5, 5, 5),
      rotation: new THREE.Vector3(Math.PI / 2, 0, 0),
      scale: 1 / 65,
      displayed: false,
    };
  },
  mounted() {
    this.$el.style.display = "block";
  },
};
</script>

<style scoped>
.HomeHTMLSprite {
  pointer-events: none !important;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
