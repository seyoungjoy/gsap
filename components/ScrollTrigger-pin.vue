<!-- Please remove this file from your project -->
<template>
  <section class="container">
  <div class="description panel blue">
    <div><h1>Layered pinning</h1>
      <p>Use pinning to layer panels on top of each other as you scroll.</p>
      <div class="scroll-down">Scroll down<div class="arrow"></div></div>
    </div>
  </div>


  <section class="panel red">
    ONE
  </section>
  <section class="panel orange">
    TWO
  </section>
  <section class="panel purple">
    THREE
  </section>
  <section class="panel green">
    FOUR
  </section>
<header>
   <a href="https://greensock.com/scrolltrigger">
     <img class="greensock-icon" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/16327/scroll-trigger-logo-light.svg" width="200" height="64" />
  </a>
</header>
  </section>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
export default {
  name: 'ScrollTrigger',
  data() {
    return {
    };
  },
  unmounted(){
    document.removeEventListener('scroll', this.scrollEvents);
  },
    mounted() {
      window.scrollTo(0,0);
      document.addEventListener('scroll', this.scrollEvents)
    // const c = document.querySelector('.boxC')
    gsap.to(this.$refs.box, {
      scrollTrigger: {
        trigger:this.$refs.box,
        start:"center bottom",
        markers:true,
        scrub:2,
        // end:"+=300",
        // toggleActions:"restart pause reverse none"
      },
      x:500,
      rotation:360,
      duration:3
    })
  },
  methods: {
    scrollEvents(){
      console.log(pageYOffset);
    }
  },

}
</script>
<style scoped>
.box-wrap{
margin-bottom:1000px;
}
.box{
  width:50px;
  height:50px;
  background: bisque;

}
</style>
