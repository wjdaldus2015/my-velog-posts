

# 포인트
✔️ 헤더 hover 이벤트
✔️ 스와이퍼 이미지별 모션 적용 + css타이핑효과
✔️ 버튼을 통한 비디오 제어
✔️ swiper를 이용한 루프 배너
✔️ css를 이용한 루프 배너

## 1.헤더 hover 이벤트
![](https://velog.velcdn.com/images/wjdaldus2017/post/f1848645-4002-45b5-a33d-e387b36742a8/image.gif)

헤더 탭 부분에 서브 메뉴가 있는 li에만 호버 이벤트를 적용시켜주었다.
 
 


## 2. 스와이퍼 이미지별 data-direction 모션 적용 + css타이핑효과
![](https://velog.velcdn.com/images/wjdaldus2017/post/93090d31-a6ea-48d9-b9de-bde493f49222/image.png)






### 스와이퍼 이미지별 data-direction 모션 적용
✅ swiper-slide가 액티브되면 이미지가 여러방향(상,하,좌,우)으로움직이게 하기.
```   <div class="bg" data-direction="top"><img src="https://woowahan-cdn.woowahan.com/new_resources/image/banner/44b95d2993754f35bc64746abd557002.jpg" alt></div>```


data-direction을 지정하고,justify-content와 align-items로 중심축을 정한다. 이미지의 길이나 너비를 원본보다 200px정도 임의로 늘려놓은 후에 transform: translateX, translateY 적용해서 이미지가 원하는 방향으로 흐를수 있도록 하였다.


### css타이핑효과 
✅css로 타이핑 효과를 구현하여 텍스트가 한 글자씩 나타나게 하기.
![](https://velog.velcdn.com/images/wjdaldus2017/post/311c07c1-6080-4bcc-a1f9-5d5a4eaf20a2/image.png)


 타이핑을 주고싶은 글자들을 word라고 정하고 그 안에서 글자들을 한 글자씩 쪼개주었다.
 ![](https://velog.velcdn.com/images/wjdaldus2017/post/90e44ab2-03bb-4a4a-a1d5-2ccfd683d1b2/image.png)
 
🌀문제점 - 애니메이션이 끝난 후, 문자의 opacity가 다시 0으로 돌아가며 사라짐. 글자가 화면에 남지 않기 때문에 애니메이션 효과가 제대로 적용된 것처럼 보이지 않음.
따라서 애니메이션이 완료된 후에도 최종 상태를 유지하고 싶다면 forwards를 반드시 적용해야 한다.
### **forwards**🌟
CSS 애니메이션에서 forwards 효과는 애니메이션이 완료된 후에도 마지막 키프레임의 스타일이 유지되도록 하는 설정이다. forwards를 적용하면 애니메이션이 끝난 후 초기 상태로 되돌아가지 않고 마지막 상태를 유지하게 된다.
`@keyframes fade {
    0%{
        opacity: 0;
    }
    100%{
        opacity: 1;
    }
}
`
## 3. 버튼을 통한 비디오 컨트롤
✅ autoplay="autoplay"로 비디오를 자동재생시키고 loop="loop"로 비디오를 루프 시킨다.
비디오를 재실행할때마다 비디오의 맨처음으로 돌아가는 부분이 어려웠는데 currentTime=0을 적용하니 원하는데로 비디오를 컨드롤 할 수 있었다.

`
$('.btn-control').click(function(){

  if ($(this).hasClass('on')) {
    $('#myVideo').get(0).currentTime=0;
    $('#myVideo').get(0).play();
    
  } else {
    $('#myVideo').get(0).pause();
  }

  $(this).toggleClass('on');
})`
✅ 버튼을 클릭할 때마다 비디오를 처음부터 재생하거나 일시정지할 수 있게 하고 display: none, display: block 으로 버튼의 아이콘을 바꿔주었다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/79b44c1b-84c7-4b8d-84dc-9d3e8e2cd907/image.png)

## 4. swiper를 이용한 루프 배너
![](https://velog.velcdn.com/images/wjdaldus2017/post/03f97756-3c24-499c-be59-2bec234704d5/image.png)


✅ swiper를 이용하여 자동으로 루프되어 계속 흘러가는 카드 슬라이드를 만들었다.
호버시에 슬라이드를 멈추고 아닐때는 다시 루프되서 흘러가게끔 jQuery hover 이벤트를 사용했다.
`const cardSlide = new Swiper('.sc-story .card-slide',{
  speed:2000,
  loop:true,
  autoplay:{
      delay:0,
  },
  slidesPerView:'auto',
})

$('.sc-story .card-slide').hover(function(){
  cardSlide.autoplay.stop()
},function(){
  cardSlide.autoplay.start()
})`
## 5. css를 이용한 무한 루프 배너
✅ 이번에는 css를 이용해서 루프 배너를 만들어 보았다.

![](https://velog.velcdn.com/images/wjdaldus2017/post/505ef65e-e532-4f87-9952-14539c1c10b2/image.gif)

`@keyframes marquee{
    0%{transform: translateX(0);}
    100%{transform: translateX(-50%);}
}`
#### @keyframes marquee🌟
CSS 애니메이션을 정의하는 규칙으로, 0%에서 100%까지의 애니메이션 단계에서 요소의 transform 속성을 변경한다. 이 애니메이션을 통해 배너의 텍스트나 이미지가 왼쪽에서 오른쪽으로 계속해서 움직이도록 설정할 수 있다.



#### linear🌟
CSS 애니메이션에서 linear는 animation-timing-function 속성의 값 중 하나로, 애니메이션의 진행 속도를 일정하게 유지하는 데 사용된다. 이 속성은 애니메이션의 각 단계 사이의 속도를 제어하여 자연스럽고 시각적으로 매끄러운 전환을 만들어줄수있다.

animation-timing-function: linear의 개념
linear 값은 애니메이션이 처음부터 끝까지 동일한 속도로 진행되도록 하고 이는 애니메이션이 시작될 때와 끝날 때 속도가 동일하다는 것을 의미한다.





 





