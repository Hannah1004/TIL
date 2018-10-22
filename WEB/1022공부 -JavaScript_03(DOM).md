# 1022공부 -JavaScript03(DOM)

- JavaScript에서 DOM객체를 동적으로 생성, 삭제, 추가 등 관리를 할수 있다.

1. #### DOM객체 접근

   - 태그의 name속성의 값으로 접근[배열]

     ```document.getElementsByName("name이름"); <input name="id">```

   - 태그의 ID속성으로 접근(많이 쓰인다.)

     ```document.getElementById("태그 id");```

   - 태그이름으로 접근

     ```document.getElementsByTagName("태그이름"); ```

2. #### DOM객체 생성, 추가 삭제

   - 태그 생성

     ```document.createElement("태그명");```

     ex) ```var x = document.createElement('p');  //<p>태그 생성```

   - text생성

     ```document.createTextNode("문자열")```

     ex)```var txt = document.createTextNode("hannah");```

   - appendChild() : 자식 노드 추가

     - 하위 노드 추가/마지막 자식 노드로 추가한다.

   - insertBefor(): 자식노드 추가

     - 특정 하위 노드 앞에 새 하위 노드를 추가한다.
     - 부모노드.insertBefore(추가할 자식 노드, 기존 자식 노드)

   - hasChildNodes() : 자식노드 유무
   - removeChild() : 자식 노드 삭제
   - replaceChild() : 자식노드를 다른 노드로 교체한다.
   - settAttribute(속성명, 속성값) : 노드의 속성 추가
   - getAttribute(속성명) : 노드의 속성 값 조회



- #### DOM접근방법

  1.  parentNode - 부모
  2.  firstChild - 첫번째자식
  3.  lastChild - 마지막자식
  4.  previousSibling- 이전형제노드
  5.  nextSibling - 다음형제노드
  6.  childNodes - 자식들
  7.  attributes -속성들