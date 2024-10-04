
# 포인트
✔️이미지 시퀀싱
✔️수평 스크롤
✔️gsap을 활용한 비디오,텍스트 scurb

# 1. GSAP과 ScrollTrigger를 활용한 이미지 시퀀싱 및 텍스트 애니메이션


✅ GSAP와 ScrollTrigger 플러그인을 활용하여 스크롤 이벤트에 따라 여러 이미지가 순차적으로 전환되며, 특정 조건에 따라 텍스트 애니메이션이 재생되는 효과를 구현하였다.

먼저, 이미지 리스트를 생성하고 총 220개의 이미지를 반복문을 통해 HTML에 추가하였다.
```
imgList=``;
for (let idx = 0; idx < 220; idx++) {
    first=(idx===0)?"on":'';
    imgList+=`<img class="${first}" src="./assets/img/Intro1080_${idx.toString().padStart(5, '0')}.png" alt>`
}

$('.sc-intro .thumb').html(imgList);
```
.sc-intro .headline .char 클래스에 속한 각 텍스트 요소가 순차적으로 y축으로 이동하는 애니메이션을 정의하며, paused: true 속성을 통해 초기에는 애니메이션이 멈춘 상태로 설정하였다.
```
//인트로 텍스트
introText = gsap.to('.sc-intro .headline .char',{
    y:0,
    stagger:0.1,
    paused:true,
})
```

 ScrollTrigger를 통해 스크롤 이벤트를 감지하고, 스크롤 위치에 따라 이미지와 텍스트 애니메이션을 제어한다.
```
ScrollTrigger.create({
    trigger:".sc-intro .sticky-wrapper",
    start:"0% 0%",
    end:"100% 100%",
    // markers:true,
    onUpdate:function(self){
        idx=Math.floor(self.progress * 219);

        if(idx > 5){
            introText.reverse();
        }else{
            introText.play();
        }

        $('.sc-intro .thumb img').eq(idx).addClass('on').siblings().removeClass('on')
    }
})
```





# 2.수평 스크롤
✅ 스크롤하는 만큼 양쪽 가로로 늘어나는 수평 스크롤을 만들고자함.
![](https://velog.velcdn.com/images/wjdaldus2017/post/41db9655-d841-424a-a16b-d0e0882bedee/image.gif)
## .wrapper 
 적응형 사이트 작업 시 최소 너비(min-width) 잡기 편하게 먼저 wrapper로 한꺼번에 감싸주고 작업하는 것이 좋다. 가장 큰 껍데기인 wrapper에 트리거를 주었다.

```
gsap.to('.top-scroll .scroll-inner',{
    scrollTrigger:{
        trigger:".wrapper",
        start:"0% 0%",
        end:"100% 100%",
        // markers:true,
       scrub:0
    },
    scaleX:1
})
```
## scaleX이란
scaleX는 CSS의 transform 속성 중 하나로, 요소의 가로 방향 크기를 조정하는 데 사용된다. 이 속성을 사용하면 요소가 X축(수평축)에서 확대되거나 축소된다.

# 3.gsap을 활용한 비디오,텍스트 scurb(stagger와 label)
✅ 맨처음에는 화면 중앙에 있다가 스크롤함에 따라 중심축은 고정되어있지만 양쪽의 너비가 늘어나는 비디오 스크럽을 구현



✅ 원하는기점에 도달했을때 안보이던 글자가 하나씩 생기면서 원래 있는 글자들이 왼쪽으로 이동하며 자동으로 가운데 정렬을 맞추는 효과를 구현하려고 하였다.

🚫 아래코드에서는 글자가 하나씩 생겨나는 효과는 줄 수 있었지만 원래 있던 글자들을 왼쪽으로 이동하며 새로생긴 글자들이 자리를 차지하는 효과는 적용할수가 없었다.
```
gsap.to('.sc-product .char',{
    scrollTrigger:{
        trigger:".sc-product",
        start:"0% 0%",
        end:"100% 50%",
        markers:true,
       scrub:0
    },
    stagger:0.1,
    scale:0,
   
})
```
🌟 피드백후에는 원래 코드에 타임라인과 라벨을 넣어 수정하였다.
라벨명을 a라고 임의로 정한다음 원하는곳에 적용하여 원하는 기점에서 두개의 효과을 같이 줄수있게 되었다.
```
textChar = gsap.timeline({
    scrollTrigger:{
        trigger:".sc-product .headline",
        start:"0% 0%",
        end:"100% 80%",
        // markers:true,
       scrub:1
    },
})

textChar.from('.sc-product .char',{
    scale: 0, // 글자가 0 크기에서 시작해 커짐
    stagger: 0.1, // 글자 하나하나에 딜레이를 줘서 차례로 애니메이션 실행
}, 'a')

textChar.from('.sc-product .word',{
    xPercent: 15 // 단어가 오른쪽에서 왼쪽으로 이동하는 효과
}, 'a')
```

✨.char: 각 글자가 scale: 0에서 커지는 애니메이션이 실행된다. stagger는 애니메이션을 순차적으로 적용하는 옵션으로, 글자 간의 시간 차이를 줄수있다.
.word: 단어 전체가 오른쪽에서 왼쪽으로 이동하는 효과를 준다.
두 애니메이션은 타임라인의 동일한 시점 'a'에서 시작되도록 설정된다.
## stagger의 효과

GSAP에서 stagger는 다수의 요소에 동일한 애니메이션을 적용할 때, 각 요소의 애니메이션 시작 시간을 일정 간격으로 지연시켜 순차적인 애니메이션 효과를 만드는 기능이다. 이 기능을 사용하면 여러 요소가 동시에 애니메이션되는 대신, 시차를 두고 순차적으로 애니메이션되도록 할 수 있으며 애니메이션에 리듬감을 주고, 더 자연스럽고 역동적인 효과를 연출하는 데 유용하다.

## label이란
GSAP (GreenSock Animation Platform)에서 라벨(Labels)은 타임라인(Timeline)에서 특정 지점을 이름으로 참조할 수 있게 하는 기능이다. 라벨을 사용하면 타임라인의 특정 지점에 쉽게 접근할 수 있어, 그 지점에서 애니메이션을 시작하거나 조작할 수 있다.

## label을 사용하는 이유
1. 가독성: 라벨을 사용하면 타임라인의 특정 지점을 더 직관적으로 참조할 수 있어 코드의 가독성이 높아진다.
2. 유지보수: 특정 지점의 이름을 통해 타임라인의 위치를 쉽게 기억하고 수정할 수 있.
3. 유연성: 라벨을 사용하면 타임라인의 위치를 정밀하게 제어할 수 있어 복잡한 애니메이션 시퀀스를 관리하기가 더 쉬워진다.



