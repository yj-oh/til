# License - GNU

## GNU GPL
- [https://ko.wikipedia.org/wiki](https://ko.wikipedia.org/wiki/GNU_%EC%9D%BC%EB%B0%98_%EA%B3%B5%EC%A4%91_%EC%82%AC%EC%9A%A9_%ED%97%88%EA%B0%80%EC%84%9C)
- GNU 일반 공중 사용 허가서(GNU General Public License, GNU GPL 또는 GPL)
- 가장 강력한 제약 조건

## 소프트웨어에 관련된 다섯 가지 의무
- 컴퓨터 프로그램을 어떠한 목적으로든지 사용할 수 있다. 다만 법으로 제한하는 행위는 할 수 없다.
- 컴퓨터 프로그램의 실행 복사본은 언제나 프로그램의 `소스 코드와 함께 판매`하거나 `소스코드를 무료로 배포`해야 한다.
- 컴퓨터 프로그램의 소스 코드를 용도에 따라 `변경할 수 있다`.
- 변경된 컴퓨터 프로그램 역시 프로그램의 소스 코드를 `반드시 공개 배포`해야 한다.
- 변경된 컴퓨터 프로그램 역시 반드시 `똑같은 라이선스`를 취해야 한다. 즉 GPL 라이선스를 적용해야 한다.

## GNU LGPL
- https://www.copyright.or.kr/information-materials/publication/research-report/download.do?brdctsno=10412&brdctsfileno=4112
- SW를 배포하는 경우 저작권 표시, 보증책임이 없다는 표시 및 LGPL에 의해 배포된다는 사실을 명시
- LGPL 라이브러리의 일부를 수정하는 경우 수정한 라이브러리의 소스코드 공개
- LGPL 라이브러리에 응용프로그램을 링크시킬(Static과 Dynamic Linking 모두) 경우 해당
  응용프로그램의 소스를 공개할 필요 없음. 다만 사용자가 라이브러리 수정 후 동일한 실행
  파일을 생성할 수 있도록 Static Linking시에는 응용프로그램의 Object Code를 제공해야 함
- 특허의 경우 GPL과 동일함

```text
LGPL은 링크하는 SW의 소스코드를 공개할 필요가 없다는 점이 GPL과 가장 큰 차이점이다.
어떠한 경우에도 LGPL SW 자체는 공개해야 하지만 LGPL SW와 링크되는 부분의 SW 소스
코드는 공개해야 할 의무가 발생하지 않으므로 기업의 입장에서는 LGPL SW를 좀 더 선호하게
된다. 사용 여부 명시 등은 GPL과 동일하게 반영하면 되고 공개해야 할 소스코드의 공개 역시
GPL과 동일한 방식을 이용하면 된다.
LGPL은 일정한 요건을 충족시키는 경우 LGPL 라이브러리를 이용하는 프로그램, 다시 말해
링킹(linking)을 통해 LGPL 라이브러리와 함께 작동하도록 설계된 프로그램을 배포할 경우에
는 소스코드를 제공하지 않아도 된다
```

## 내가 이해한 바로는
### GPL 
  - 어떤 목적으로든 사용 가능
  - 사용하거나 변경하여 사용할 경우 무조건 동일한 GNU GPL 적용
  - 소스코드 공개 의무
### LGPL
  - 어떤 목적으로든 사용 가능
  - 단순 활용 시 공개 의무 없음
  - 수정한 소스 코드는 LGPL로 공개 의무
