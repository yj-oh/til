# AWS 도메인 연결
### 1. Route 53 대시보드 접속
![Route 53 대시보드 접속](.%5B%5D_aws_도메인_연결_images/01.png)

### 2. 호스팅 영역 - 호스팅 영역 생성
![호스팅 영역 생성](.%5B%5D_aws_도메인_연결_images/02.png)

### 3. 도메인 이름 입력
![도메인 이름 입력](.%5B%5D_aws_도메인_연결_images/03.png)
##### 다시 호스팅 영역으로 가보면 호스팅 영역이 생성된 것을 확인할 수 있다.
![](.%5B%5D_aws_도메인_연결_images/04.png)
##### 도메인 이름을 눌러서 클릭하면 NS 유형의 값 4개가 보임.
![](.%5B%5D_aws_도메인_연결_images/07.png)

### 4. 가비아 네임서버 설정
##### 위의 값 4개를 가비아 네임서버에 설정해준다.
![](.%5B%5D_aws_도메인_연결_images/05.png)

![](.%5B%5D_aws_도메인_연결_images/06.png)

### 5. 레코드 생성
![](.%5B%5D_aws_도메인_연결_images/08.png)
##### 다음
![](.%5B%5D_aws_도메인_연결_images/09.png)
##### 단순 레코드 정의
![](.%5B%5D_aws_도메인_연결_images/10.png)