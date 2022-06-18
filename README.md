# GSAP width Nuxt
## `gsap.fromTo()`
- 시작부분에서 끝부분 까지의 애니메이션 설정 가능.
```jsx
gsap.fromto(".box", 
  { opacity:0}, //fromVars
  { opacity:0.5, duration:1, ease:"elastic"} //toVars
)
```

## ScrollTrigger
- https://greensock.com/docs/v3/Plugins/ScrollTrigger
### usage
```jsx
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
```
```jsx
    const c = document.querySelector('.boxC')

    gsap.to(c, {
      scrollTrigger:"c",
      x:400,
      rotation:360,
      duration:3
    })
// 스크롤시 c에 도착했을 때 자동으로 트리거됨... wow
```
### toggleAction
- restart: 스크롤 트리거 반복 재생
- reverse : 스크롤 역방향시 애니메이션도 역방향으로 바뀜.
```jsx
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
```

### start end
- start:"400px" -> scrollY가 400px를 넣을 때 시작.
- start:"top center" -> viewport 기준 중간에 닿았을 때 시작.
❓반응형에서 start를 어떻게 지정해야하지? px로는 안될거같은데

### markers
- scroller-start, scroller-end 지점을 표시해줌.

### scrub
- 스크롤에 따라 함께 움직임.
- scrub:true
- scrub : number, 스크롤을 잡는데 걸리는 시간을 지정해줄 수 있음. 훨씬 부드럽다.
```jsx
// timeline을 이용해 scrub 효과에 3가지 모션을 차례대로 줄 수 있다.
let tl = gsap.timeline({
  scrollTrigger:{
    trigger:".c",
    start:"top center",
    end:"top 100px",
    scrub:3,
    markers:true
  }
});
tl.to(".c"{
  x:400,
  rotation:360,
  ease:"none",
  duration:3
})
.to(".c",{
  backgroundColor:"purple",
  duration:1
})
.to(".c",{
  x:0,
  duration:3
})
```

## Issue
### 1. Cannot use import statement outside a module
- ssr 사용시 build시 transpile 목록에 gsap를 추가해야함.(in nuxt.config)
```jsx
build: {
    ...
    transpile: ['gsap'],
},
```
- If using server side rendering, you may also need to check if the process is on the server or the client:
```jsx
import { gsap } from "gsap";
import { MorphSVGPlugin } from "gsap/MorphSVGPlugin";

if (process.client) {
  gsap.registerPlugin(MorphSVGPlugin);
}
```

### 2. vue에서 scroll event 추가시 mounted/unmounted 활용법
- [Reference](https://thisiscoke.tistory.com/entry/Vue-life-cycle%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%98%EC%97%AC-scroll-event%EB%A5%BC-%EC%A0%81%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90)
- window.scrollTo(0,0)을 통해 화면전환시 스크롤 좌표를 0,0으로 리셋
- eventlistener에 scroll시 호출할 함수를 추가
```jsx
 mounted() {
    window.scrollTo(0, 0);
    document.addEventListener('scroll', this.scrollEvents);
  },

```
- mounted에서 추가했던 eventListener를 제거해줘야한다. 안그러면 router-link를 통해 화면을 전환해도 메모리에서 여전히 동작하고 있기때문에 다른 method와 충돌이 발생할 수 있다.
```jsx
 unmounted() {
    document.removeEventListener('scroll', this.scrollEvents);
  },

```

## Reference
- https://lpla.tistory.com/107
- https://velog.io/@yesslkim94/GSAP-ScrollTrigger
- scrollTrigger demos
    - https://greensock.com/st-demos/?d=19
