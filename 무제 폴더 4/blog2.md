
# 포인트
#### ✔️ cherryinvestments 클론코딩 후 cyber truck의 이미지와 텍스트를 사용
#### ✔️ cusor animation
#### ✔️ 스크롤에 따른 텍스트 투명도 조절 

## 1.스크롤에 따른 텍스트 투명도 조절 
![](https://velog.velcdn.com/images/wjdaldus2017/post/3d78c7aa-2ff2-4879-a543-7ab7f84620b2/image.gif)

```
gsap.to('.sc-visual svg',{
    scrollTrigger:{
        trigger:".sc-visual ",
        start:"0% 0%",
        end:"100%",
       scrub:0,
       pin:true
    },
    opacity:1,
   
})

```
🌟 scrub - 스크롤을 위아래로 움직일 때마다 모션을 주기 위해 사용했디.
스크롤 했을때 텍스트가 나타나게끔 opacity: 1 로 구현



## 2.커서 이벤트
✅ 사용자 경험(UX)을 높이기 위해 마우스 커서와 연동된 인터랙티브한 효과를 구현하는 하고자하였고  jQuery와 GSAP을 활용하여 마우스 움직임에 따라 커서가 움직이고, 특정 요소에 마우스를 올렸을 때 해당 이미지가 변하는 애니메이션 효과를 보여주었다.

```
$(window).mousemove(function(e){
    // console.log(e.clientX);
    // console.log(e.clientY);
    x=e.clientX;
    y=e.clientY;

    gsap.to('.cursor',{
        x:x,
        y:y,
    })

})


$('.prd-item').hover(function(){
    idx=$(this).index();
    $('.cursor .img-area').addClass('show');
    $('.cursor .img-area .item').eq(idx).addClass('on').siblings().removeClass('on')

},function(){
    $('.cursor .img-area').removeClass('show');
})

```


📛 이미지가 해당 li에 맞게 바뀌지 않았다.
hover 이벤트가 발생할 때마다 .item 클래스가 적용된 모든 요소에 on 클래스가 추가되거나 제거된다. 원래 의도는 특정 idx에 해당하는 .item만 on 클래스를 가지도록 하는 것인데, 이 방식에서는 전체 .item 요소가 동시에 클래스 변경의 영향을 받게 되는 문제가 발생하였다.

🌟 피드백 후 eq메소드를 사용하여 ``` 해당 인덱스에 해당하는 이미지에 on 클래스를 추가하여 이미지를 표시
    $('.cursor .img-area .item').eq(idx).addClass('on').siblings().removeClass('on'); ``` 부분을 수정하였다.
    
###     ✔️eq메소드란?
    
eq() 메서드는 jQuery에서 특정 요소 집합 내에서 인덱스 번호에 해당하는 요소를 선택할 때 사용되는 메서드입니다. jQuery의 선택자(selector)는 여러 개의 요소를 선택할 수 있는데, 그 중 특정 위치에 있는 요소만을 선택하고자 할 때 eq()를 사용합니다.
###     ✔️eq 메소드의 특징
1.0부터 시작하는 인덱스

eq(0)은 첫 번째 요소를 선택하고, eq(1)은 두 번째 요소를 선택하는 식으로 진행된다.

2.음수 인덱스

eq(-1)과 같이 음수를 사용할 수도 있다. 이 경우, 선택한 요소 집합에서 마지막 요소가 선택된다. 예를 들어 eq(-1)은 마지막 요소, eq(-2)는 뒤에서 두 번째 요소를 선택한다.

3.단일 요소 반환

eq()는 jQuery 객체의 집합에서 특정 요소를 선택하여 단일 jQuery 객체를 반환한다. 이는 선택된 요소에 대해 추가적인 메서드 체이닝을 쉽게 할 수 있도록 해준다.
    



