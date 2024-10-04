
# 1. 시맨틱(Semantic)이란 
"의미론적인" 의 뜻을 가지며 마크업(Markup)이란 HTML 태그로 문서를 작성하는 것을 말한다. 따라서, 시맨틱 마크업이란 의미를 잘 전달하도록 문서를 작성하는 것을 말한다.

## 시맨틱 마크업의 장점

#### ✅ 가독성과 유지보수성 향상
시맨틱 태그는 의미 있는 요소로 구분되므로, 코드를 읽거나 유지보수할 때 이해하기 쉬워진다. header, nav, main, footer 와 같은 시맨틱 태그를 사용하면 웹 페이지의 구조를 쉽게 이해할 수 있다.

#### ✅ 검색 엔진 최적화(SEO)에 도움
시맨틱 태그는 웹 페이지의 구조와 내용을 더 명확하게 전달할 수 있으므로, 검색 엔진이 페이지의 콘텐츠를 이해하기 쉬워진다. 이렇게 함으로써 검색 엔진은 해당 웹 페이지의 내용을 더 잘 인식하고, 노출할 수 있다.

#### ✅ 웹 접근성 향상
시맨틱 태그는 스크린 리더와 같은 보조 기술을 사용하는 사용자들이 웹 페이지를 더 쉽게 이해하도록 도와준다. 시맨틱 태그는 특정한 목적을 가진 요소로 구성되어 있으므로, 사용자들이 웹 페이지의 구조와 내용을 더 쉽게 파악할 수 있다.

#### ✅ 코드의 의미가 명확해짐
시맨틱 태그를 사용하면, 코드의 의미가 더 명확하게 전달된다. 이렇게 함으로써 코드를 작성하는 개발자들이 코드를 더 쉽게 이해하고, 유지보수하기 쉬워진다.

클래스 작명규칙
>#### 의미⭕️
section — 섹션 (ex. sc-login)
group — 그룹 (ex. group-header)
area — 영역잡아줄때 (ex. control-area)
wrap — 작은단위 (ex. banner-wrap)
box — 더 작은단위 (ex. dict-box)

>#### 의미❌
col-left, col-right
header-top, header-bottom
footer-inner,inner

>사용목적이 있는 작명
link - 링크이동이 목적 (ex. link-more, view-more)
btn - 스크립트 작용이 목적 (ex. btn-prev, btn-next)

>리스트
ul - (ex. ooo-list)
li - (ex. ooo-item)

# 2. IR기법
IR(Image Replacement) 기법은 이미지를 볼 수 없는 사용자에게 적절한 대체 텍스트를 제공하는 것으로 이는 웹 접근성 준수를 위한 스크린 리더 사용자뿐 아니라 검색 엔진의 효과적인 내용 수집을 위해서도 필요하다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/18a060f1-6b45-474a-924f-1ec66f0195b4/image.png)
```
.blind{
    position: absolute;
    width: 1px;
    height: 1px;
    overflow: hidden;
    clip: rect(0,0,0,0);
    margin: -1px;
}
```

# 3.IS기법
사전적으로는 조각난 이미지 파일들을 하나의 스프라이트 이미지로 병합 후 background-position 속성을 이용하여 이미지를 배치하는 방법이다. 웹 문서 전송 속도를 높이는 기법이고 용량이 적어 웹브라우저의 로딩 속도를 줄여준다.


#### ✅common css
![](https://velog.velcdn.com/images/wjdaldus2017/post/597283b1-2978-4bb2-90a4-b465457386c3/image.png)

#### ✅layout css
![](https://velog.velcdn.com/images/wjdaldus2017/post/b29d0d6f-7400-42b5-804f-2acd5f8d54d6/image.png)




IS기법과 IR기법을 함께 사용하면 서버로의 요청 횟수를 최소화하여 웹 페이지의 로딩 속도를 줄일 수 있고, 이미지들을 관리하기 쉬워진다.


# 4. WAI-ARIA
마우스와 같은 포인팅 장비를 사용하기 힘든, 스크린 리더를 사용하는 사용자들에게 동적 컨텐츠, javascript, ajax, vue, react 등과 같이 페이지를 새로고침 하지 않고도 페이지의 내용과 데이터가 바뀌는 영역에 역할, 속성, 상태 정보를 추가하여 동적인 컨텐츠에 보다 원활하게 접근하고 페이지에 접근성을 높여 여러 사용자들에게 원활한 페이지 이용을 도와준다.
또한 WAI-ARIA는 단순 HTML로 표현할 수 없는 의미들을 태그에 부여하여 시각적인 불편함이 있는 사용자들게 일반적인 구조의 HTML에서 필요한 요소에 적절한 정보를 전달받아 원활하게 페이지 탐색 및 이용을 하도록 도와준다.

✅ role
HTML의 요소 종류와 역할이 서로 맞지 않을 때, 어떤 역할을 하는 요소인지 명시해줄 때 사용할 수 있는 속성(attribute)이다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/028b14cc-9f07-4060-8f84-64fd5c92d2f3/image.png)
✅ aria-selected
탭메뉴를 구성할때 현재 어떤 탭이 선택되어 있는지도 알 수 있어야 한다. 이럴 때 사용하는 속성이 바로 여러 개의 선택 가능한 요소중에서 선택 상태인 요소를 표시할 수 있는  aria-selected 라는 속성이다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/fcbadc3b-0412-426d-8702-6fb481a8e2b2/image.png)



### WAI-ARIA의 장점
1. 요소(Element) 및 컴포넌트에 누락된 의미를 명확하게 제공할 수 있다.

2. 스크린리더 등 보조기기 사용성을 향상 시킨다.

3. 논리적인 구조 설계와 구조의 시각화가 가능하다.

4. 구조에 의미를 부여함으로써 페이지 영역의 빠른 탐색이 가능하다.

5. 동적 컨텐츠의 식별이 가능하다.

6. 상태 변화 발생시 사용자 에이전트는 사용하는 API에 적절한 이벤트 알림을 제공한다.



