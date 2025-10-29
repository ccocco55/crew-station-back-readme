# 👨‍👩‍👧‍👦Crew station

# 함께 여행하고, 기록하고, 나누며, 성장할 수 있도록 돕는 여행 동행 플랫폼

## 1. 🎯기획 의도

<img style = 'width: 1500px' src='../gb_0900_icm/crew_station_발표/슬라이드4.JPG'>
<img style = 'width: 1500px' src='../gb_0900_icm/crew_station_발표/슬라이드5.JPG'>

현대의 청년들은 **혼자 여행**에 대한 로망을 갖고 있지만,  
실제로는 아래와 같은 문제를 겪고 있습니다.

-   💸 **높은 여행비**로 인한 경제적 부담
-   😔 **언어와 안전 문제**로 인한 불안감
-   🧳 **혼자 여행의 외로움과 심리적 부담**

또한, 요즘 청년들은 단순한 관광보다  
“**경험을 기록하고, 공유하며, 스스로 성장하는 여행**”을 원합니다.  
이와 동시에 **여행 중 소규모 수익을 창출할 수 있는 기회**에 대한 수요도 높습니다.

이에 Crew Station은

> **“청년들이 함께 여행하고, 기록하고, 나누며, 성장할 수 있는 공간”** 을 목표로 기획되었습니다.

## 2. 💡기대 효과

<img style = 'width: 1500px' src='../gb_0900_icm/crew_station_발표/슬라이드7.JPG'>

### 1️. 경제적 부담 완화와 기회 형평성 제고

-   **크루 매칭 및 공동 숙박**을 통해 여행 비용을 나눠 부담함으로써 청년층의 경제적 장벽을 낮춤
-   여행지에서의 **기념품 판매 기능**으로 여행 중 소규모 수익 창출 가능

### 2️. 창업적 감각 함양

-   여행 중 판매 데이터를 기반으로 **상품 선호도, 반응, 트렌드 분석 가능**
-   실제 소비자 반응을 통해 **시장성 있는 아이템 발굴 및 사업성 검증**

### 3️. 콘텐츠 기반 성장

-   여행 일기 기능을 통해 **개인의 여행 경험을 콘텐츠로 기록 및 공유**
-   **일기 → 기록 → 콘텐츠 → 영향력**으로 이어지는 자연스러운 성장 구조 형성

### 4️. 심리적 안정감 제공

-   낯선 여행지에서도 **함께할 크루**를 통해 안정감 확보
-   **혼자 여행의 외로움과 불안을 완화**하며 건강한 여행 문화 조성

---

## 3. 🧰프로젝트 사용 툴

### Backend

-   Spring Boot, Spring Security, JWT
-   Java
-   JDK 17.0.10
-   Spring Session & Cache (Redis)
-   OAuth2 Social Login
-   Springdoc OpenAPI (Swagger UI)
-   Thymeleaf, AOP, Lombok
-   MyBatis

### Database

-   MyBatis
-   PostgreSQL
-   Redis

### HTML Engine

-   Thymeleaf

### Infra

-   AWS S3
-   AWS IAM
-   AWS EC2

### External APIs

-   Boot Pay API
-   CoolSms API
-   Rest API
-   Naver Developer API
-   Kakao Developer API
-   Goolge Developer API
-   Kakao Daum Postcode API
-   SMTP Gmail API

### Tool

-   IntelliJ IDEA
-   DBeaver
-   Git / GitHub / Sourcetree
-   Slack
-   PostMan

### Test

-   Junit5

## 4. 🗂️ERD

<img style = 'width: 1500px' src='포폴/이미지/erd.png'>

## 5. 👩🏻‍💻담당 업무

<img src='포폴/이미지/back.png'>

### 백엔드

▶ 회원가입

-   이메일 중복 검사
-   이메일, 휴대폰, 비밀번호, 생년월일, MBTI 입력 형식 검사
-   API를 이용한 주소 찾기
-   필수 정보 입력 여부 검사
-   조건 충족 시 회원가입
-   핸드폰 번호 인증 번호 발송
-   소셜 회원가입: 카카오, 네이버, 구글 API를 연동한 OAuth2 간편 회원가입

▶ 로그인

-   이메일, 비밀번호 Spring Security, JWT를 사용하여 로그인 기능 구현
-   소셜 로그인: 카카오, 네이버, 구글 API를 연동한 OAuth2 간편 로그인
-   Redis에 refreshToken 저장 → accessToken 만료 시 재발급 처리

▶ 게스트 로그인

-   주문번호, 핸드폰 번호 Spring Security, JWT를 사용하여 로그인 기능 구현
-   Redis에 refreshToken 저장 → accessToken 만료 시 재발급 처리

▶ 로그아웃

-   로그아웃 시 Redis에 블랙리스트 등록 → 만료되지 않은 access token 차단
-   access token과 refresh token 삭제 → 클라이언트/서버에서 모두 무효화

▶ 비밀번호 재설정

-   가입 된 이메일 확인 정보 있을 경우 다음 단계 이동
-   확인 코드 이메일 발송, 코드 일치 시 다음 단계 이동
-   비밀번호 변경

## 6. 🛠️오류 상황들

#### **( 1 )** 회원과 같은 서비스가 되어버리는 게스트

🌩문제 상황🌩  
<img src="포폴/이미지/게스트 글 작성.png">

게스트 로그인 시에도 게시글 작성 페이지에 접근이 가능했습니다.
(게스트 계정은 작성 기능을 사용할 수 없어야 함)

🚨문제 원인🚨  
게스트의 access token이 일반 회원으로 잘못 인식되어
작성 페이지 접근이 허용되었습니다.

🚀해결 방법🚀

1. GuestInterceptor 생성

<img src="포폴/이미지/guestInterceptor1.png">
<img src="포폴/이미지/guestInterceptor2.png">

-   로그인한 사용자의 username이 이메일 형식인지 확인 후
-   이메일 형식이 아니면 게스트 계정으로 분류 했습니다.

2. 게스트 계정이 회원 전용 페이지에 접근하려고 하면

<img src="포폴/이미지/web1.png">

<img src="포폴/이미지/web2.png">

-   로그아웃 처리 후
-   로그인 페이지로 리다이렉트 하였습니다.

✅ 결과: 게스트 계정은 회원 전용 기능에 접근할 수 없도록 안전하게 제한되었습니다.

---

#### 소셜 로그인 후 일반 회원 로그인 불가

🌩문제 상황🌩  
<img src="포폴/이미지/회원가입후로그인.png">
<img src="포폴/이미지/문제2.png">

소셜 로그인(카카오, 네이버, 구글 등) 이후 로그인 페이지에서
일반 로그인 시도 시 정상적인 계정 정보 입력에도 로그인이 되지 않았습니다.

🚨문제 원인🚨  
소셜 로그인 시 생성된 쿠키(name, provider)가 브라우저에 남아있어
일반 로그인 시 기존 소셜 세션 정보와 충돌이 발생했습니다.

🚀해결 방법🚀

1. resetCookies 메서드 추가

<img src="포폴/이미지/쿠키 삭제 메소드.png">

-   모든 쿠키 및 Redis에 저장된 refreshToken을 삭제하는 메서드 생성했습니다.

2. service.js 수정

<img src="포폴/이미지/쿠키_서비스.png">

-   로그인 요청 전 resetCookies를 비동기(async)로 실행하도록 수정했습니다.

3. event.js 수정

<img src="포폴/이미지/쿠키 삭제 사용.png">

-   로그인 페이지 로드 시점에 `memberService.resetCookies();` 호출하여
    기존 쿠키 및 세션 데이터 초기화했습니다.

✅ 결과: 로그인 페이지 진입 시 모든 쿠키와 Redis refreshToken이 삭제되어
소셜 로그인 후에도 일반 로그인이 정상적으로 동작하게 되었습니다.

#### **(2)** 소셜 로그인 같은 이메일 사용시 같은 회원으로 인식

🌩문제 상황🌩  
<img src="포폴/이미지/기존코드.png">

서로 다른 소셜 로그인이 하나의 이메일을 사용하는 경우, 신규 회원 가입 창이 아닌 기존 회원으로 인식되어 바로 로그인이 되는 문제가 발생했습니다.

🚨문제 원인🚨  
회원 조회 시 이메일만을 기준으로 판단했기 때문에, 소셜 제공자가 다르더라도 이메일이 같으면 동일 회원으로 처리되는 로직이었습니다.

🚀해결 방법🚀

1. MemberMapper.xml 수정

<img src="포폴/이미지/mapper-xml.png">

-   provider 조건을 추가하여 이메일과 소셜 제공자를 함께 조회하도록 수정했습니다.

2. MemberMapper.java 수정

<img src="포폴/이미지/mapper-java.png">

-   provider를 매개변수로 추가하여 DAO 계층에서 전달 가능하도록 변경했습니다.

3. MemberDAO.java 수정

<img src="포폴/이미지/dao.png">

-   이메일과 provider를 함께 조건으로 사용하여 정확한 회원 조회가 가능하도록 수정했습니다.

4. CustomOAuth2UserService 수정

<img src="포폴/이미지/service.png">

-   OAuth2 인증 과정에서 registrationId를 통해 소셜 제공자(Google, Naver, Kakao 등)를 식별하고, 사용자 정보에서 provider 값을 추출하여 회원 조회 시 이메일과 함께 비교하도록 개선했습니다.

#### **(2-1)** BadSqlGrammarException 오류 발생

🌩문제 상황🌩

<img src="포폴/이미지/6-2_오류.png">

`BadSqlGrammarException` 예외가 발생했습니다.

🚨문제 원인🚨

<img src="포폴/이미지/6-2_기존코드.png">
<img src="포폴/이미지/6-2_기존코드2.png">

PostgreSQL에서는 `ENUM`이 사용자 정의 타입(`TYPE`)으로 처리되는데, Java 코드에서 `provider` 값을 단순 `String`으로 전달하면서 타입 불일치가 발생했습니다. 이로 인해 SQL 문법 오류가 발생한 것입니다.

🚀해결 방법🚀

<img src="포폴/이미지/변경코드2.png">
<img src="포폴/이미지/변경코드.png">

`MemberProvider` Enum 클래스에서 `provider` 값을 매핑하여, 문자열이 아닌 Enum 객체로 변환한 후 DAO에 전달하도록 수정했습니다. 이를 통해 PostgreSQL의 ENUM 타입과 정확히 일치하는 값으로 쿼리를 실행할 수 있게 되었고, 타입 불일치로 인한 오류를 해결했습니다.

## 7. 🧪QA 테스트

-   테스트 케이스 설계 및 실행 절차를 기반으로 QA 테스트 문서를 작성하고 기능별 검증을 수행했습니다.
-   **JUnit5를 활용한 단위 테스트 및 통합 테스트**를 통해 애플리케이션의 안정성과 기능 완성도를 검증했습니다.

<img src="포폴/이미지/qa.png" />

## 8. 📝총평

🌟 **기획 : 꼼꼼함의 중요성**

기획은 처음부터 꼼꼼히 준비해도 예상치 못한 변수가 항상 생겼습니다.
기획 의도에서 벗어나는 순간마다 팀원들과의 지속적인 대화와 토론을 통해 문제를 해결했고,
그 과정에서 더 나은 방향을 찾아가며 완성도 높은 서비스를 만들어낼 수 있었습니다.

🌟 **협업 : 소통이 곧 완성도**

주석만으로는 화면을 만든 개발자의 의도와 맥락을 완전히 이해하기 어렵다는 것을 배웠습니다.
팀원 간의 충분한 소통을 통해 서로의 의도를 명확히 맞추는 것이
결국 품질 높은 결과물과 효율적인 개발 과정으로 이어짐을 깨달았습니다.

🌟 **미래 : 성장에 대한 확신**

프로젝트를 하나씩 완성해 나가면서 코드가 점점 다듬어지고,
문제를 해결할 수 있는 시야가 넓어지는 과정을 경험했습니다.
이 과정이 재미있고 도전적이었으며, 앞으로 더 나은 코드를 작성할 수 있을 것이라는 확신을 갖게 되었습니다.

🌟 기술적 성장

-   Spring Security + Jwt를 이용한 인증·인가 흐름에 대한 이해도를 높였습니다.
-   Redis를 활용한 세션 관리 최적화 및 응답 속도 개선했습니다.

📌 **작성자:** 임채민 &nbsp;&nbsp;&nbsp;&nbsp; **TEAM:** crew station  
📅 **기간:** 2025.09.09 ~ 2025.10.21
