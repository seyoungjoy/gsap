<!-- Please remove this file from your project -->
<template>
  <section class="container">
    <div class="row">
      <div class="col-12">
        <div class="box a">a</div>
        <div class="box b">b</div>
        <div class="box boxC" ref="box">c</div>

      </div>
    </div>
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
  methods: {

  },
  mounted() {
    const c = document.querySelector('.boxC')
    gsap.to(c, {
      scrollTrigger: {
        trigger:"c",
        toggleActions:"restart pause reverse none"
      },
      x:400,
      rotation:360,
      duration:3
    })
  }
}
</script>
<style scoped>
.box{
  width:50px;
  height:50px;
  background: bisque;
  margin-bottom:1000px;
}
</style>
