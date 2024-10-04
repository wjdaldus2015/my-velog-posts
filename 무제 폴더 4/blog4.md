

# 포인트 

✔️ swiper 재생/정지 버튼 기능,tab 버튼 이벤트 
✔️ popup 컨텐츠 히든 크로스브라우징 처리
✔️ 웹접근성 향상
✔️ btn-top 페이지 최상단 이동
✔️ slideToggle 함수를 사용한 드롭다운 메뉴 구현


# 1. swiper 재생/정지 버튼 기능,tab 버튼 이벤트 
![](https://velog.velcdn.com/images/wjdaldus2017/post/e47a031c-92a5-4971-95ea-ff4b302bfa5b/image.png)


  ✅ 활성화된 버튼과 슬라이드를 연동하고 컨트롤 영역을
  navigation - 슬라이드를 수동으로 넘길 수 있도록 nextEl을 next로, prevEl을 prev로 설정해주고 이를 각각 다음과 이전 슬라이드를 나타낼수 있게 구현
pagination - type을 fraction으로 설정하고 슬라이드의 총 개수와 현재 슬라이드의 번호를 표시하였다.
```
const visualSlide1 = new Swiper ('.sc-visual .news .swiper',{
    loop:true,
    autoplay:{
        delay:1000
    },
    navigation:{
        nextEl:".next",
        prevEl:".prev",
    },
    pagination:{
        el:".fraction",
        type:"fraction"
    }
})
```
✅ if문을 사용하여 슬라이드의 재생/정지기능을 구현했다.
```
$('.sc-visual .news .autoplay').click(function(){

    if($(this).hasClass('active')){
        visualSlide1.autoplay.start();

    }else{
        visualSlide1.autoplay.stop();
    }
    $(this).toggleClass('active');
    
})
```
✅ 주요뉴스, 시민참여 탭을 생성하고 각 슬라이드를 만들어서 겹쳐놓은후 탭을 눌렀을때 해당되는 슬라이드만 보이게 구현하였다.
```
$('.sc-visual .title').click(function(e){
    e.preventDefault();

    // $('.sc-visual .content').removeClass('active');
    $(this).parent().addClass('active').siblings().removeClass('active');

})
```
# 2. 크로스브라우징 처리
✅  popup content를 스크롤 할때 뒤에 보이는 html부분이 같이 스크롤 되는걸 막으려고 html에 hidden이라는 클래스를 추가하였다.
```
hidden{
    overflow: hidden;
    height: 100%;
}

```

🌟 하지만 위의 코드는 윈도우에서만 작동을 하기때문에 크로스브라우징 처리를 위해 아래코드로 수정을 하였다.
```
html.hidden,
html.hidden body{
    overflow: hidden;
    height: 100%;
}
```
![](https://velog.velcdn.com/images/wjdaldus2017/post/7b7bb28d-48e0-4671-a8b2-36878b04d4aa/image.png)
# 3. 웹접근성 향상
![](https://velog.velcdn.com/images/wjdaldus2017/post/30734b3c-0628-428d-a7c0-d617a97d51b3/image.png)

✅ 웹접근성 향상을 위해 리더기가 읽는 순서를 고려하며 순서대로 제목(주요서비스)-내용(list)-더보기(전체누리집)순으로 구현하였다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/e9ca1b45-bb67-4fd3-8d63-45f534ff4a03/image.png)


# 4. btn-top 페이지 최상단 이동
✅ 처음에는 버튼이 보이지 않다가 화면에서 스크롤을 조금 내렸을때부터 버튼이 아래에서 윗쪽방향으로 나타나고, 그 버튼을 눌렀을때 스크롤이 페이지 최상단으로 이동하게 구현하고 싶었다.
```
$('.btn-top').click(function(){
    window.scrollTo({top:0,behavior:'smooth'})
});
```
🌟 피드백을 받은 후에 아래 소스를 추가했고
```
$(window).scroll(function(){
    curr = $(this).scrollTop();
    if(curr > 0){
        $('.fix-btn').addClass('show')
    }else{
        $('.fix-btn').removeClass('show')
    }
})
```
✅ css로 transition, opacity등의 효과를 넣어주었다.

![](https://velog.velcdn.com/images/wjdaldus2017/post/2287db51-448b-4e7a-bcf4-1558e1f87e03/image.png)

# 5.드롭다운 메뉴 구현
![](https://velog.velcdn.com/images/wjdaldus2017/post/722772f3-0f0d-48bc-a17e-f037c065e075/image.png)

✅ 메뉴 타이틀을 눌렀을때 해당 svg가 로테이션 되고 위로 sub메뉴가 나오게 구현하고자 하였다.
slideUp, slideDown 기능을 이용하여 하나의 서브메뉴는 컨트롤했지만 this를 제외한 다른 title들을 컨트롤 하지 못했다.
```
$('.btn-title').click(function(e){
    e.preventDefault();
    if($(this).hasClass('on')){
        $(this).removeClass('on').slideUp();

    }else{
        $('.btn-title').removeClass('on').slideUp();
        $(this).addClass('on').slideDown();
    }

})

```


🌟 피드백 후에 siblings('.sub')을 추가해서 원하는 대로 드롭 다운 메뉴를 구현할 수 있었다.


```
$('.btn-title').click(function(e){
    e.preventDefault();
    if($(this).hasClass('on')){
        $(this).removeClass('on').siblings('.sub').slideUp();

    }else{
        $('.btn-title').removeClass('on').siblings('.sub').slideUp();
        $(this).addClass('on').siblings('.sub').slideDown();
    }

})
```









  

            
            
            
            