<!-- Please remove this file from your project -->
<template>
  <section class="container">
    <div class="row">
      <div class="col-12">
        <div class="box-wrap">
          <div class="box a">a</div>
        </div>
        <div class="box-wrap">
          <div ref="box" class="box boxC">b</div>
        </div>


        <div class="box-wrap">
          <div class="box">c</div>
        </div>
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
