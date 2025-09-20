# 무무랩 결제 시스템

Polar API를 사용한 무무랩 서비스 결제 페이지입니다.

## 기능

- **무무랩 홈페이지 구독**: 월 9,900원 (KRW)
- **무무랩 후원하기**: 일회성 3,000원 (KRW)
- 반응형 디자인
- 실시간 결제 처리
- 결제 완료 페이지

## 파일 구조

```
├── index.html          # 메인 결제 페이지
├── success.html        # 결제 완료 페이지
└── README.md          # 설정 가이드
```

## 설정 방법

### 1. Polar 계정 설정

1. [Polar.sh](https://polar.sh)에서 계정을 생성합니다.
2. 조직(Organization)을 생성합니다.
3. API 키를 발급받습니다.

### 2. 제품 생성

Polar 대시보드에서 다음 제품들을 생성해야 합니다:

#### 무무랩 홈페이지 구독
- **제품 ID**: `mumulab_home_subscription`
- **제품명**: 무무랩 홈페이지 구독
- **가격**: 9,900 KRW
- **타입**: 구독 (월간)

#### 무무랩 후원하기
- **제품 ID**: `mumulab_support`
- **제품명**: 무무랩 후원하기
- **가격**: 3,000 KRW
- **타입**: 일회성 결제

### 3. 코드 설정

`index.html` 파일에서 다음 값들을 실제 값으로 교체하세요:

```javascript
// 실제 토큰과 조직 ID로 교체
const POLAR_ACCESS_TOKEN = 'your_polar_access_token_here';
const POLAR_ORGANIZATION_ID = 'your_organization_id';
```

### 4. 웹훅 설정 (선택사항)

결제 완료 후 서버에서 처리가 필요한 경우 Polar 웹훅을 설정하세요:

1. Polar 대시보드에서 웹훅 설정
2. 엔드포인트 URL 설정
3. 이벤트 타입 선택 (payment.completed 등)

## 보안 고려사항

### 프로덕션 환경에서는:

1. **API 키를 클라이언트 사이드에 노출하지 마세요**
   - 백엔드 서버에서 Polar API 호출
   - 클라이언트는 백엔드 API 호출

2. **HTTPS 사용**
   - 모든 결제 관련 페이지는 HTTPS로 서빙

3. **도메인 검증**
   - Polar에서 허용된 도메인만 결제 페이지 호스팅

## API 엔드포인트

### Polar API 주요 엔드포인트

- **체크아웃 세션 생성**: `POST /v1/checkouts/`
- **결제 상태 확인**: `GET /v1/payments/{payment_id}`
- **구독 관리**: `GET /v1/subscriptions/`

## 테스트

### 로컬 테스트

1. 웹 서버 실행:
   ```bash
   # Python 3
   python -m http.server 8000

   # Node.js (http-server 패키지 필요)
   npx http-server
   ```

2. 브라우저에서 `http://localhost:8000` 접속

### 결제 테스트

Polar의 테스트 모드를 사용하여 실제 결제 없이 테스트 가능합니다.

## 문제 해결

### 자주 발생하는 문제

1. **CORS 오류**
   - 브라우저에서 직접 Polar API 호출시 발생
   - 해결: 백엔드 서버를 통한 API 호출

2. **API 키 오류**
   - 잘못된 API 키 또는 권한 부족
   - 해결: Polar 대시보드에서 API 키 확인

3. **제품 ID 오류**
   - 존재하지 않는 제품 ID
   - 해결: Polar 대시보드에서 제품 ID 확인

## 지원

- Polar 공식 문서: https://docs.polar.sh
- API 레퍼런스: https://api.polar.sh/docs

## 라이선스

이 프로젝트는 MIT 라이선스를 따릅니다.