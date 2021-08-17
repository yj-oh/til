# article vs section
- HTML5 시멘틱 태그

## 👉 \<article>
- 홀로 사용될 수 있는 내용
- 독자적으로 이미 완성형인 내용
- e.g) 블로그 포스팅, 뉴스 기사, 댓글

## 👉 \<section>
- 서로 관련 있는 것들을 묶어주기 위한 용도

## 💬 생각
- `article`에 `section`이 포함될 수도 있고, `section`에 `article`이 포함될 수도 있다.
- 나는 여러 개의 관련 있는 `article`을 `section`으로 묶는다는 개념이 더 옳다고 생각했는데,
  이런 글을 봤다.
  - [\<article>과 \<section> 및 \<div> 의 적절한 사용에 관한 고찰](https://developern.tistory.com/entry/how-to-article-section-div-tag)
  ```text
  위와 같은 기본적인 의미를 생각 한다면 <section>안에 <article>이 여러 개 들어가는 것은 
  조금 부자연스러울 수 있다. 왜냐하면 서로 관련 있는 내용을 모아 놓아야 할 <section>안에 
  각각이 독립된 <article>이 들어가 서로 다른 내용의 독립 <article>이 배치되기 때문이다.
  따라서 <article>안에 <section>이 들어가는 것이 자연스럽다.
  ```
  - 각각은 독립적이지만 같은/비슷한 영역의 것일 수 있지 않나? 
  - 왜 `article`이 '서로 다른 내용' 이라는 전제를 깔고 있는지 모르겠다.
  - 예를 들면 뉴스 기사와 광고 배너들은 각각이 `article`로, 
    뉴스 기사 전체를 하나의 `section`, 광고 전체도 하나의 `section`으로 묶어 구분하는 용도로
    사용한다면 각 태그의 기본 용도에 어긋남이 없어보인다.
  - 쓰루!
- [\<section> 버리고 HTML5 \<article> 써야 하는 이유](https://webactually.com/2020/03/03/%3Csection%3E%EC%9D%84-%EB%B2%84%EB%A6%AC%EA%B3%A0-HTML5-%3Carticle%3E%EC%9D%84-%EC%8D%A8%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0/)
  - 이 글이 도움이 되었다.
  - 마크업 세계가 이렇게나 심오한 것인지 처음 알았다. 흥미로워서 한 번쯤 읽어봄직하다.
