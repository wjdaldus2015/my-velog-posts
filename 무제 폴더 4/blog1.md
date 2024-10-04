#### ✔️ GSAP Draggable을 사용한 리스트 드래그 기능 
#### ✔️ JSON을 활용한 데이터 바인딩 기법
## 1. GSAP Draggable을 사용한 리스트 드래그 기능 
![](https://velog.velcdn.com/images/wjdaldus2017/post/459e75bc-f777-4203-93bf-f1b2425ae8c5/image.gif)


### 1-1. 각 상품 아이템의 너비 및 개수 계산
그냥 스와이퍼를 적용하게 되면 끝도 없이 드래그 되기 때문에 드래그 가능 범위를 정확하게 계산하여 설정해야했다.

```
let w = $(this).find('.prd-item').width();
let cnt = $(this).find('.prd-item').length;
```

⚫️ w: 각 상품 아이템(.prd-item)의 너비를 계산하여 변수 w에 저장합니다.
⚫️ cnt: 해당 프로모션 그룹 내에 있는 상품 아이템의 개수를 계산하여 cnt에 저장한다.
이를 통해 나중에 아이템들을 얼마나 많이 보여줄지, 드래그 가능 범위를 설정하는 데 사용된다.

### 1-2.상품 개수가 짝수일 경우 처리
```
if (cnt % 2 === 0) {
    cnt -= 1;
}
```
⚫️ 이 코드는 상품의 개수가 짝수일 때 마지막 하나를 제외하여 홀수로 만든다.

### 1-3.홀수 인덱스 요소를 추출
```
let oddIndexes = []; 
for (let i = 0; i < cnt; i += 2) {
    oddIndexes.push(i);
}
```
⚫️ 이 부분에서는 홀수 인덱스를 찾는 작업을 수행한다.
i += 2로 루프를 돌면서 0, 2, 4 등 짝수 인덱스에 해당하는 아이템을 배열 oddIndexes에 저장
상품 리스트의 특정 부분에 간격(gap)을 두는 데 사용된다.

### 1-4.gap 값을 설정
```
oddIndexes.forEach((value, index) => {
    gap = index;
});
```
⚫️oddIndexes 배열을 순회하면서 각 아이템의 인덱스를 gap으로 설정한다.

### 1-5.전체 아이템 개수 계산
```
total = gap + 1;
```
⚫️ 총 드래그할 수 있는 아이템의 개수는 gap + 1로 설정한다.
즉, gap은 인덱스의 마지막 값이므로 총 개수를 gap + 1로 계산

### 1-6.드래그 가능한 리스트 설정
```
Draggable.create($(this).find('.prd-list'), {
    type: "x",
    bounds: {
        minX: 0,
        maxX: -(total*w) + $('.wrapper').width() - (gap*5) - 32,
    }
});
```
⚫️ Draggable.create(): GSAP의 Draggable 기능을 사용하여 prd-list 요소를 수평(x축)으로 드래그할 수 있게 만든다.
type: "x"는 드래그가 X축(수평 방향)으로만 가능하다는 의미이다.
🌟bounds 옵션:
minX: 0: 드래그가 가능한 최소 X축 값으로, 0은 더 이상 왼쪽으로 드래그되지 않도록 설정하였다.
maxX: 드래그 가능한 최대 X축 값으로 
-(total*w)는 모든 상품의 총 너비를 계산해 전체 리스트를 얼마나 드래그할 수 있을지 결정한다.
$('.wrapper').width()는 리스트가 표시되는 영역의 너비입니다.
(gap*5)는 상품 간의 간격을 고려한 값입니다.
-32는 추가로 .prd-list에 padding: 0px 16px; 값이 있어 똑같이 양쪽에 패딩값을 주기위해 *2를 했다.


## 2. jQuery와 Fetch API를 사용한 JSON 데이터 바인딩
✔️ JSON 파일을 가져와서 상품 데이터를 동적으로 HTML에 바인딩하고자 하였다. 이를 위해 fetch API를 사용해 데이터를 불러오고, forEach 문을 통해 데이터를 각 상품 리스트에 삽입하는 과정이다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/f2893772-eb4a-41c9-8795-49111826f585/image.png)
✅ 메뉴를 담고 있는 ul은 그대로 두고 li들을 잘라내서 js 파일에 알맞게 넣는다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/0582f260-23e5-4521-b830-2f6e935be269/image.png)
✅ 메뉴의 데이터들을 담고 있는 json 파일을 만들어준 후에
이 여러개의 prd-list들을 반복문(foreach)을 돌려서 적용시켜주면 된다.

### 2-1.
✔️ 우선 fetch API를 사용해 product.json 파일을 비동기로 가져온다. fetch는 데이터를 서버에서 불러와 처리할 때 매우 유용하며, 프로미스(Promise)를 반환하므로 then 구문을 통해 데이터를 처리한다.
    
⚫️  fetch: product.json 파일을 서버에서 가져온다.
	res.json(): 응답 데이터를 JSON 형태로 파싱한다.
	json: 파싱된 JSON 데이터를 변수로 받는다.
    
![](https://velog.velcdn.com/images/wjdaldus2017/post/99e1abfe-5430-40c4-b438-4e6a9ec6e843/image.png)

    
###  2-2.
✔️ fetch로 데이터를 가져온 후, 각 상품 리스트(prdList1Arr, prdList2Arr, prdList3Arr)에 해당하는 배열을 forEach 문을 사용해 순회하며 HTML 템플릿을 생성하였다. 각 상품에는 이미지, 브랜드명, 가격 정보가 포함

⚫️ prdList1Arr.forEach(): prdList1Arr 배열에 있는 각 상품에 대해 반복문을 돌면서 HTML 템플릿을 생성한다.

⚫️ percentEl: 할인율이 있는 상품의 경우, 할인율을 표시하는 HTML 요소를 생성한다.
isPercent: 할인율이 존재하는지 확인한 후, 할인율이 있으면 템플릿에 포함시키고, 없으면 빈 값으로 처리.
list1List: 반복문을 통해 각각의 prd-item 요소를 누적해서 저장한다.

![](https://velog.velcdn.com/images/wjdaldus2017/post/d95d6098-e554-40b0-ae37-98cb4974174d/image.png)
### 2-3.
✔️위와 동일한 방식으로 prdList2Arr와 prdList3Arr에 대해서도 데이터를 처리하고, 각각의 리스트를 HTML로 변환하여 저장한다.
### 2-4.
✔️이제 생성된 HTML 템플릿을 DOM에 삽입하여 페이지에 렌더링한다. 각각의 리스트(list1List, list2List, list3List)는 #list1, #list2, #list3라는 ID를 가진 요소에 삽입

⚫️ $('#list1').html(list1List): 생성된 list1List HTML을 #list1 요소에 삽입하여 화면에 표시한다.

⚫️ 마지막으로 draggList() 함수를 호출해 리스트를 드래그할 수 있는 기능을 추가해준다.
![](https://velog.velcdn.com/images/wjdaldus2017/post/c910bd05-4511-4bd3-bb82-7149896fc9d9/image.png)










    



