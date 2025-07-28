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
  <summary><strong>1. NFT 이미지가 관리자 및 마이페이지에서 표시되지 않는 문제</strong></summary>
  • <strong>문제 상황</strong>: 관리자 페이지와 사용자 마이페이지에서 NFT 이미지가 정상적으로 로드되지 않고 빈 화면 또는 오류 발생
  <br/>
  • <strong>원인 분석</strong>: 서버 저장 이미지 URL과 외부 저장소 경로 불일치로 이미지 접근 실패
  <br/>
  • <strong>해결 방법</strong>: <br/>
    • 이미지 URL 유효성 검증 로직 추가로 잘못된 주소 사전 탐지 <br/>
    • 정적 파일 경로 및 외부 IPFS 주소 관리 체계 개선으로 일관성 유지 <br/>
    • 이미지 캐시 정책과 CORS 설정 점검하여 원활한 로드 보장 <br/>
 • <strong>효과</strong>: 외부 저장소 연동 시 주소 관리와 접근성 중요성 체감, 이미지 자원 관리가 사용자 경험에 직접 영향
</details>

<details>
  <summary><strong>2. 외래키 제약조건으로 인한 삭제 오류 및 데이터 무결성 문제</strong></summary>
  • <strong>문제 상황</strong>: NFT 데이터 물리적 삭제 시 외래키 제약조건 위반으로 연관 데이터가 남아 삭제 실패 및 서버 에러 발생
  <br/>
  • <strong>원인 분석</strong>: 연관 엔티티 미삭제 또는 DB에 CASCADE 옵션 미설정으로 인한 문제
  <br/>
  • <strong>해결 방법</strong>: <br/>
    • deletedAt 타임스탬프 필드 활용하는 소프트 딜리트 방식 적용 <br/>
    • 연관 엔티티에도 모두 소프트 딜리트 적용하여 참조 무결성 유지 <br/>
    • 조회 시 삭제 플래그 설정된 데이터 필터링해 사용자 노출 차단 <br/> 
    • 필요 시 복구 기능 지원으로 데이터 안정성 및 운영 편의성 강화 <br/>
 • <strong>효과</strong>: 소프트 딜리트는 외래 키 제약 문제 회피와 데이터 무결성 보장에 효과적이며, 운영 안정성을 크게 개선
</details>

<details>
  <summary><strong>3. 사용 후 UI가 새로고침해야만 상태 변경 반영 문제</strong></summary>
  • <strong>문제 상황</strong>: NFT 쿠폰 사용 후 화면이 즉시 업데이트되지 않고 새로 고침 필요
  <br/>
  • <strong>원인 분석</strong>: React 상태 관리에서 변경된 상태 값 즉시 갱신 안 되어 리렌더링 발생하지 않음
  <br/>
  • <strong>해결 방법</strong>: <br/>
   • useEffect 훅으로 상태 변화 감지 및 리렌더링 로직 추가 <br/>
   • 상태 변경 함수 호출 후 데이터 재 요청 또는 로컬 상태 동기화 수행 <br/>
 • <strong>효과</strong>: 사용자 경험은 실시간 피드백과 반응성에 크게 의존, 상태 관리와 렌더링 최적화가 매우 중요

</details>
<hr/>

### 느낀 점

![느낀점](https://github.com/user-attachments/assets/4d5c2c87-a796-4fc6-9f0b-229fc096eb65)
