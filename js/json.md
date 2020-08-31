## JSON이란?

JSON(제이슨, JavaScript Object Notation)은 속성-값 쌍( attribute–value pairs and array data types (or any other serializable value)) 또는 "키-값 쌍"으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷이다.

<br>

## JSON Parser 예시

```jsx
let personArray = new Array();

// 사람 정보
let personInfo = new Object();
personInfo.name = "송강호";
personInfo.age = "25";
personInfo.gender = "남자";
personInfo.nickname = "남궁민수";
personArray.push(personInfo);

personInfo = new Object();
personInfo.name = "전지현";
personInfo.age = "21";
personInfo.gender = "여자";
personInfo.nickname = "예니콜";
personArray.push(personInfo);

//책 정보
let bookArray = new Array();

bookInfo = new Object();
bookInfo.name = "사람은 무엇으로 사는가?";
bookInfo.writer = "톨스토이";
bookInfo.price = "100";
bookInfo.genre = "소설";
bookInfo.publisher = "톨스토이 출판사";
bookArray.push(bookInfo);

bookInfo = new Object();
bookInfo.name = "홍길동전";
bookInfo.writer = "허균";
bookInfo.price = "300";
bookInfo.genre = "소설";
bookInfo.publisher = "허균 출판사";
bookArray.push(bookInfo);

bookInfo = new Object();
bookInfo.name = "레미제라블";
bookInfo.writer = "빅토르 위고";
bookInfo.price = "900";
bookInfo.genre = "소설";
bookInfo.publisher = "빅토르 위고 출판사";
bookArray.push(bookInfo);

//사람, 책 정보를 넣음
let totalInfo = new Object();
totalInfo.persons = personArray;
totalInfo.books = bookArray;

let jsonInfo = JSON.stringify(totalInfo);
console.log(jsonInfo);

/*
{
    "persons":[
                 {"name":"송강호","age":"25","gender":"남자","nickname":"남궁민수"},
                 {"name":"전지현","age":"21","gender":"여자","nickname":"예니콜"}
              ],
    "books":[
               {"name":"사람은 무엇으로 사는가?","writer":"톨스토이","price":"100","genre":"소설","publisher":"톨스토이 출판사"},
               {"name":"홍길동전","writer":"허균","price":"300","genre":"소설","publisher":"허균 출판사"},
               {"name":"레미제라블","writer":"빅토르 위고","price":"900","genre":"소설","publisher":"빅토르 위고 출판사"}
            ]
}
*/
```

<br>

_reference_

[위키백과 - JSON](https://ko.wikipedia.org/wiki/JSON)

[JavaScript 에서 JSON 생성](https://huskdoll.tistory.com/11)
