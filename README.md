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

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```
