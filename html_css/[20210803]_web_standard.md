# 웹 표준
- 브라우저 제조사 간의 기술 전쟁
- W3C(world wide web consortium) 설립
- 공통 웹 기술에 대한 표준 정의
- **'가능한 많은 사람이 웹을 사용하게 하는 것'**
- 모든 브라우저에서 모든 사용자에게 똑같이 보이게 하는 것이 아니다.
- 단계적 향상
  - 모든 사용자에게 기본 기능 제공, 좋은 성능을 가진 브라우저를 사용하는 사용자에게만 추가적인 기능 제공
  - e.g) 웹 표준안을 지키는 브라우저에서는 섀도 이펙트가 보이게, 지키지 않는 브라우저에서는 이펙트 포기
- 콘텐트(HTML), 디자인(CSS), 기능(JS)의 분리
- 브라우저가 이해할 수 있게, 의미 있게 구성할 것

* 웹 표준이 중요한 이유
  - https://www.thisisgame.com/webzine/nboard/213/?n=56672
  - 만화다. 재밌음.

## DOCTYPE
- 마크업 언어 표기
- 버전 표기
- 구분 규칙의 엄격성 표기
- 필수 : 선언이 없을 경우 구버전의 브라우저는 비 표준 관용 모드로 페이지를 렌더링

Doctype | Declaration
--- | ---
html5 | <!DOCTYPE html>
HTML 4.01 Strict | <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
HTML 4.01 Transitional | <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
XHTML 1.0 Strict | <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
XHTML 1.0 Transitional | <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
XHTML 1.1 | <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
- 프로젝트에는 strict 사용할 것

## 웹 표준 검사
- https://validator.w3.org/
