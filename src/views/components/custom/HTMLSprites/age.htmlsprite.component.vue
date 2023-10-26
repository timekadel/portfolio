<template>
  <div class="LabelHTMLSprite">
    <Transition name="fade">
      <div v-if="displayed" style="opacity-100">
        <h1 class="text-white opacity-90 z-10 text-6xl sm:text-6xl md:max-w-2xl lg:text-7xl xl:text-8xl font-bold">
          Here's a fun fact about me:
        </h1>
        <br />
        <h3 v-html="subtext" class="z-10 text-white text-2xl sm:text-2xl xl:text-3xl max-w-xl font-thin opacity-90"/>
        <span class="input"></span>
      </div>
    </Transition>
  </div>
</template>

<script>
import * as THREE from "three";
import HTMLSpriteMixin from "@/mixins/HTMLSprite.mixin.js";

export default {
  name: "AgeHTMLSprite",
  mixins: [HTMLSpriteMixin],
  data() {
    return {
      position: new THREE.Vector3(1.2, 0.5, 2.2),
      rotation: new THREE.Vector3(Math.PI / 2, -0.1, 0),
      scale: 1 / 300,
      displayed: false,
      age: {
        years: 0,
        months: 0,
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0
      },
      prompts:[
        this.computeBirthDateSting,
        ()=>"I _develop* things for the _web* 🕸️.        ",
        ()=>"I _love* electronics* ✨.        ",
        ()=>"Unbiasedly, _Vue.js* > _React* 🤫.         ",
        ()=>"C is amazing, pointers aren't scary 👻.         ",
        ()=>"I ❤️ _WebGL* 🪄.        ",
      ],
      promptIndex: 0,
      sentenceIndex: 0,
      subtext: ""
    };
  },
  methods: {
    computeBirthDateSting() {
      const birthdate = new Date(756537900 * 1000);
      var diff = new Date(new Date(Date.now()).getTime() - birthdate.getTime());
      this.age.years = diff.getUTCFullYear() - 1970;
      this.age.months = diff.getUTCMonth();
      this.age.days = diff.getUTCDate();
      this.age.hours = diff.getUTCHours();
      this.age.minutes = diff.getUTCMinutes();
      this.age.seconds = diff.getUTCSeconds();
      return `I'm _${this.age.years}* ${this.handlePlural(this.age.years,'year')}, _${this.age.months}* ${this.handlePlural(this.age.months,'month')} and _${this.age.days}* _${this.handlePlural(this.age.days,'day')}* old.        `;
    },
    prompt(){
      setTimeout(()=>{
        let currentPrompt = this.prompts[this.promptIndex]();
        if(this.sentenceIndex >= currentPrompt.length){
          this.sentenceIndex = 0;
          this.promptIndex = (this.promptIndex + 1) % this.prompts.length
          currentPrompt = this.prompts[this.promptIndex]();
        }
        this.subtext = currentPrompt.substring(0, ++this.sentenceIndex).replaceAll("_","<b>").replaceAll("*","</b>") + "|"
        this.prompt();
      }, (Math.random() * (5 - 1) + 1) * 30)
      
    },
    handlePlural(value, word) {
      return `${word}${(value > 1) ? 's' : ''}`;
    }
  },
  mounted() {
    this.$el.style.display = "block";
    this.computeBirthDateSting();
    this.prompt();
  },
};
</script>

<style scoped>
.LabelHTMLSprite {
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
.input{
  width: 75%;
  height: 18px;
  display: flex;
  border-bottom: 2px solid rgba(255,255,255,.5);
}
</style>
