# KoNLPy 설치 for macOS (+ class 비교)

## ❓ KoNLPy
- 파이썬 한글 형태소 분석기
- `코엔엘파이`라고 읽는다고 한다.
- 공식 한글 문서 : https://konlpy-ko.readthedocs.io/ko/v0.5.2/
    - 프로젝트의 철학이 인상 깊다.
        ```text
         이 프로젝트에는 세 가지 철학이 있습니다:
          - 사용법이 간단해야 한다.
          - 누구나 쉽게 이용할 수 있어야 한다.
          - “인터넷 민주주의는 효과적이다.”
         위의 항목 중 하나라도 어긋나는 것이 있다면 제보 부탁드립니다.
        ```

## ⚙️ 설치
- `Python`과 `Java JDK`가 설치되어 있어야 함.
    - 널리고 널린게 자료라서 설치 방법은 생략한다.
- `KoNLPy` 설치 방법은 기록할 것도 없이 매우 간단하지만 
  나는 파이썬이 익숙치 않아서 꼭꼭 씹어먹기 위해 기록한다.

### 1. JPype 설치
```
pip3 install JPype1-py3
```

### 2. KoNLPy 설치
```
pip3 install konlpy
```

### 3. 설치 확인
- 아래 코드를 실행해보자.
```
from konlpy.utils import pprint
from konlpy.tag import Kkma

kkma = Kkma()
pprint(kkma.sentences('hello, world'))
```
![](.%5B20201225%5D_install_konlpy_images/6083a6b5.png)

## ※ 5가지 클래스가 있다.
>- Hannanum Class
>- Kkma Class
>- Komoran Class
>- Mecab Class
>- Okt Class
- Hannanum Class
  - JHannanum is a morphological analyzer and POS tagger written in Java, 
    and developed by the Semantic Web Research Center (SWRC) at KAIST since 1999.
- Kkma Class
  - Kkma is a morphological analyzer and natural language processing system 
    written in Java, developed by the Intelligent Data Systems (IDS) 
    Laboratory at SNU.
- Komoran Class
  - KOMORAN is a relatively new open source Korean morphological analyzer 
    written in Java, developed by Shineware, since 2013.
- Mecab Class
  - MeCab, originally a Japanese morphological analyzer and POS tagger 
    developed by the Graduate School of Informatics in Kyoto University, 
    was modified to MeCab-ko by the Eunjeon Project to adapt to the 
    Korean language.
- Okt Class (Twitter)
  - Open Korean Text is an open source Korean tokenizer written in Scala, 
    developed by Will Hohyon Ryu.

## 🤔 뭘 쓰지?
- https://konlpy.org/ko/v0.4.3/morph/
  - 이 링크를 참고하여, `Okt` class를 쓰기로 결정했다.
