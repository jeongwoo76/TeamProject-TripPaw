# TripPaw
![스크린샷_27-7-2025_13413_](https://github.com/user-attachments/assets/b9537060-3310-4097-aa00-5bdfd132e12a)

## Team GitHub
- https://github.com/syeon279/tripPaw
### 목차
- 1️⃣ [프로젝트 개요](#프로젝트-개요)
- 2️⃣ [기술 스택](#기술-스택)
- 3️⃣ [담당 기능](#담당-기능)
- 4️⃣ [데이터 베이스 설계](#데이터-베이스-설계)
- 5️⃣ [트러블 슈팅](#트러블-슈팅)
- 6️⃣ [느낀 점](#느낀-점)

<hr/>

### 프로젝트 개요
반려동물을 동반한 여행을 즐기고자 하는 사용자들을 위한 **맞춤형 여행 추천 & 예약 플랫폼**입니다.
사용자의 여행 스타일과 관심 지역에 따라 최적의 여행 경로를 추천하며, 다른 사용자들의 여행 코스를 그대로 따라가며 일괄 예약 및 결제도 가능하도록 설계되었습니다.

**"기획 배경"** <br/>
반려동물을 동반한 여행을 준비할 때, 일반적인 여행 플랫폼에서의 정보는 제한적이며 불편함이 많음을 느꼈습니다.
이를 해결하고자, 반려동물과 함께 안전하고 즐겁게 여행할 수 있는 정보, 예약, 커뮤니티 기능을 갖춘 플랫폼이 필요하다고 판단하여 본 프로젝트를 기획하게 되었습니다.

<hr/>

### 기술 스택
🌐 **Front-End**
- Next.js 15.3.5
- React 18.20.0
- Ant Design (antd) 4.23.16
- styled-components 5.3.11
- Axios 1.9.0
- Kakao Map API 1.2.0
- Stomp.js 7.1.1
- WebSocket 1.6.1
- dnd-kit 6.3.1
- SortAble 1.15.6
- date-fns 4.1.0
- html2canvas

🖥️ **Back-End**
- Spring Boot 2.7.14
- Java 11
- Spring Security 2.7.14
- Spring Data JPA 2.7.14
- MyBatis 2.3.1
- MySQL 8.0
- Redis 2.7.14
- Thymeleaf 3.0.15
- RESTful API 2.7.14
- JWT Token 0.1.15
- Lombok 1.18.28
- PortOne 결제 API
- imPort API 0.2.3
- OpenAI API 2.3.0
- web3j 4.8.7

📦 **기타**
- Spring Boot Admin
- WebSocket 서버 통신
- WSS 기반 실시간 알림 기능
- AI 연동(OpenAI)
<hr/>

### 담당 기능
#### 📺 시연 영상 (이미지 클릭시 유튜브로 이동됩니다.)

[![Watch the video](https://github.com/user-attachments/assets/3f173be9-4ed1-431f-948b-c23a41413926)](https://youtu.be/i2rlSeZK0rM)

1. 예약 및 결제 CRUD 설계 및 기능 구현
2. 추천받은 경로, 다른 사용자의 경로대로 일괄 예약 기능 구현
3. 일괄 예약한 내역 일괄 결제 기능 구현
4. 통합 결제 api를 연동하여 카드,카카오페이,토스페이 등 다양한 결제 기능 구현
5. 예약에 자동 만료일 부여 – 만료시 다른 사용자도 예약가능

<hr/>

### 데이터 베이스 설계

<img width="512" height="261" alt="unnamed" src="https://github.com/user-attachments/assets/5b162ea3-fc78-4a21-9435-673eec262693" />

<hr/>

### 트러블 슈팅
<details>
  <summary><strong>1. 예약 날짜 일괄 비활성화 오류</strong></summary>
  • <strong>문제 상황</strong>: 단일 장소에서 예약한 날짜가 전체 예약 건에 일괄 적용, 모든 장소의 동일한 날짜가 예약 불가능 처리
  <br/>
  • <strong>원인 분석</strong>: 장소(place_id) 조건 없이 날짜만을 기준으로 비활성화, 모든 장소에 동일한 날짜 비활성화 적용
  <br/>
  • <strong>해결 방법</strong>: 예약 비활성화 로직에서 장소 식별자(place_id) 조건 포함<br/> → JOIN 구문을 통해 장소별 예약 날짜 필터링<br/> → 장소별로 독립된 비활성화 날짜 처리 가능

</details>
<details>
  <summary><strong>2. 결제 시 예약 정보 누락</strong></summary>
  • <strong>문제 상황</strong>: 결제 진행 시, 예약 정보(장소명, 가격 등)가 화면에 미출력 혹은 null 값으로 표시되는 문제 발생
  <br/>
  • <strong>원인 분석</strong>: 결제 매퍼에서 예약id만 조회하고, 이에 따른 예약 상세 정보를 Join하여 가져오지 않아 필요한 정보가 누락
  <br/>
  • <strong>해결 방법</strong>: 결제 매퍼에 예약 테이블과의 JOIN 구문을 추가<br/> → 예약 ID 뿐만 아니라 관련된 예약 상세 정보(장소, 시간, 금액 등)를 함께 조회하도록 수정

</details>
<details>
  <summary><strong>3. 결제 취소 및 환불 시 예약 상태 미반영</strong></summary>
  • <strong>문제 상황</strong>: 결제 취소 또는 환불을 진행해도 해당 예약 상태가 여전히 "예약 중"으로 유지되는 문제 발생
  <br/>
  • <strong>원인 분석</strong>: 결제 및 예약 상태 간 연결 관계 미설정<br/> → 결제 취소 처리 시 예약 상태 업데이트 실패
  <br/>
  • <strong>해결 방법</strong>: 예약 상태와 결제 상태를 Enum 타입으로 정의<br/> → 예약 상태가 취소일 경우에만 결제 취소 또는 환불을 가능하게 하는 로직 구성<br/> → 결제 상태 변경과 예약 상태 변경을 동기화

</details>
<details>
  <summary><strong>4. 일괄 예약 시 경로 정보 미조회</strong></summary>
  • <strong>문제 상황</strong>: 여러 장소를 포함하는 일괄 예약 시, 경로 정보 조회 실패<br/> → 예약 데이터가 null로 저장되는 오류 발생
  <br/>
  • <strong>원인 분석</strong>: 초기 테스트에서는 더미 데이터를 기반으로 경로 ID만 연결하여 기능 확인<br/> → 실제 경로 정보 테이블과의 관계 설정이 누락
  <br/>
  • <strong>해결 방법</strong>: 예약 테이블이 경로 정보 테이블과 관계를 맺도록 수정<br/> → JOIN 구문을 통해 일괄 예약 시 각 경로의 정보를 조회할 수 있도록 개선

</details>
<details>
  <summary><strong>5. 일괄결제 취소, 환불 오류</strong></summary>
  • <strong>문제 상황</strong>: 일괄 결제의 취소 또는 환불 요청 미처리
  <br/>
  • <strong>원인 분석</strong>: 일괄 결제는 여러 예약을 경로 ID 기준으로 묶어 총 금액을 계산하는 구조<br/> → 결제 테이블에 예약 ID 저장 불가<br/> → 환불 처리 시 참조할 예약 정보가 미존재
  <br/>
  • <strong>해결 방법</strong>: 결제 테이블 중심이 아닌, 각 예약이 결제 ID를 참조하도록 구조 개선<br/> → 환불 로직에서는 동일 결제id를 가지는 예약들을 묶어 처리하도록 변경<br/> → 일괄 결제에 대한 환불도 정상 작동하게 개선

</details>

<hr/>

### 느낀 점

![느낀점](https://github.com/user-attachments/assets/b69e5bc8-eeae-4727-a1e0-213f5c335e50)
