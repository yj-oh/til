# Unit Test naming conventions
- https://dzone.com/articles/7-popular-unit-test-naming
- 위 링크의 내용을 내 맘대로 번역함.

---

- 간략한 정보를 레퍼런스성으로 정리한 글이니 자세한 내용은 아래 링크 참고.
  - [Naming Standards for Unit Tests](http://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html)
  - [Naming Unit Tests Responsibly](http://googletesting.blogspot.in/2007/02/tott-naming-unit-tests-responsibly.html)
  - [What are some popular naming conventions for unit tests?](https://stackoverflow.com/questions/96297/what-are-some-popular-naming-conventions-for-unit-tests)
  - [Unit Tests Naming Best Practices](https://stackoverflow.com/questions/155436/unit-test-naming-best-practices)
  - [GivenWhenThen Technique](https://martinfowler.com/bliki/GivenWhenThen.html)

## 1. MethodName_StateUnderTest_ExpectedBehavior
### 💎 메소드명_테스트상태_예상결과
- 코드 리펙토링하면서 메소드명 변경되면 테스트 이름도 변경되어야 함.
- 그렇지 않으면 나중에 이해하기 어려워진다는 의견이 있다.
>- isAdult_AgeLessThan18_False
>- withdrawMoney_InvalidAccount_ExceptionThrown
>- admitStudent_MissingMandatoryFields_FailToAdmit

## 2. MethodName_ExpectedBehavior_StateUnderTest
### 💎 메소드명_예상결과_테스트상태
- 위와 비슷한 형태지만 일부 개발자들은 이 네이밍 기술을 사용할 것을 권유한다.
- 마찬가지로 메소드명이 바뀌면 나중에 이해하기 어려워진다.
>- isAdult_False_AgeLessThan18
>- withdrawMoney_ThrowsException_IfAccountIsInvalid
>- admitStudent_FailToAdmit_IfMandatoryFieldsAreMissing

## 3. test[Feature being tested]
### 💎 test[테스트할 기능]
- 테스트할 기능이 이름의 일부로 사용되어 쉽게 읽을 수 있게 해준다.
- 그러나 "test" 접두사가 중복된다.
>- testIsNotAnAdultIfAgeLessThan18
>- testFailToWithdrawMoneyIfAccountIsInvalid
>- testStudentIsNotAdmittedIfMandatoryFieldsAreMissing

## 4. Feature to be tested
### 💎 테스트할 기능
- 테스트 메소드는 애너테이션을 이용해 식별하므로 기능을 간단히 작성하는 것이 좋다.
  또 테스트를 문서의 대체 형식으로 만들고 코드 악취를 피할 수 있으므로 권장된다.
>- IsNotAnAdultIfAgeLessThan18
>- FailToWithdrawMoneyIfAccountIsInvalid
>- StudentIsNotAdmittedIfMandatoryFieldsAreMissing

## 5. Should_ExpectedBehavior_When_StateUnderTest
### 💎 Should_예상결과_When_테스트상태
- 테스트를 쉽게 읽을 수 있게 해준다.
>- Should_ThrowException_When_AgeLessThan18
>- Should_FailToWithdrawMoney_ForInvalidAccount
>- Should_FailToAdmit_IfMandatoryFieldsAreMissing

## 6. When_StateUnderTest_Expect_ExpectedBehavior
### 💎 When_테스트상태_Expect_예상결과
>- When_AgeLessThan18_Expect_isAdultAsFalse
>- When_InvalidAccount_Expect_WithdrawMoneyToFail
>- When_MandatoryFieldsAreMissing_Expect_StudentAdmissionToFail

## 7. Given_Preconditions_When_StateUnderTest_Then_ExpectedBehavior
### 💎 Given_전제조건_When_테스트상태_Then_예상결과
- BDD(Behavior-Driven-Development)의 일부로 개발된 네이밍 컨벤션에 기초한다.
  테스트를 세 파트로 나누어 전제조건, 테스트 상태, 예상 결과 제시한다.
>- Given_UserIsAuthenticated_When_InvalidAccountNumberIsUsedToWithdrawMoney_Then_TransactionsWillFail
