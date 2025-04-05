# Weather Wizard

<div align="center">
  <img src="https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB">
  <img src="https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white">
  <img src="https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB">
  <img src="https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white">
</div>

<div align="center">
  <h3>GitHub Actions를 활용한 CI/CD 파이프라인 구축 실습 프로젝트</h3>
</div>

## 📖 개요

Weather Wizard는 사용자 위치 기반의 날씨 정보를 제공하는 웹 애플리케이션으로, GitHub Actions를 활용한 CI/CD 파이프라인 구축을 실습하기 위한 토이 프로젝트입니다. 이 프로젝트를 통해 코드 작성부터 테스트, 배포까지의 전체 개발 프로세스를 자동화하는 방법을 배울 수 있습니다.

## 🌟 주요 기능

- 현재 위치 기반 실시간 날씨 정보 제공
- 도시 검색을 통한 날씨 정보 조회
- 5일 날씨 예보 제공
- 반응형 디자인으로 모바일/데스크톱 환경 지원

## 🛠️ 기술 스택

### 프론트엔드
- **React**: 사용자 인터페이스 구축
- **JavaScript/ES6+**: 프로그래밍 언어
- **CSS3**: 스타일링
- **Axios**: API 요청 처리

### 백엔드
- **Node.js**: 서버 환경
- **Express**: 웹 프레임워크
- **OpenWeatherMap API**: 날씨 데이터 소스

### CI/CD
- **GitHub Actions**: 자동화된 워크플로우
- **Jest**: 자동화된 테스트
- **ESLint**: 코드 품질 검사
- **GitHub Pages**: 프론트엔드 배포
- **Heroku**: 백엔드 배포

## 🏗️ 프로젝트 구조

```
weather-wizard/
├── frontend/                   # 프론트엔드 코드
│   ├── public/
│   ├── src/
│   │   ├── components/         # React 컴포넌트
│   │   ├── services/           # API 호출 서비스
│   │   ├── styles/             # CSS 스타일
│   │   ├── pages/              # 페이지 컴포넌트
│   │   └── __tests__/          # 테스트 코드
│   ├── .github/
│   │   └── workflows/
│   │       └── frontend-ci.yml  # 프론트엔드 CI/CD 워크플로우
│   └── README.md
│
├── backend/                    # 백엔드 코드
│   ├── src/
│   │   ├── controllers/        # 요청 처리 컨트롤러
│   │   ├── routes/             # API 라우트
│   │   ├── services/           # 날씨 API 서비스
│   │   └── index.js            # 서버 엔트리 포인트
│   ├── tests/                  # 테스트 코드
│   ├── .github/
│   │   └── workflows/
│   │       └── backend-ci.yml   # 백엔드 CI/CD 워크플로우
│   └── README.md
│
└── README.md                   # 프로젝트 메인 README
```

## 🚀 시작하기

### 사전 요구사항

- Node.js 14.x 이상
- npm 6.x 이상
- OpenWeatherMap API 키 ([여기에서 무료로 얻을 수 있습니다](https://openweathermap.org/api))

### 설치 및 실행

#### 프론트엔드

```bash
# 프론트엔드 디렉토리로 이동
cd frontend

# 의존성 설치
npm install

# 개발 서버 실행
npm start
```

브라우저에서 http://localhost:3000 으로 접속하여 애플리케이션을 확인할 수 있습니다.

#### 백엔드

```bash
# 백엔드 디렉토리로 이동
cd backend

# 의존성 설치
npm install

# .env 파일 생성 및 API 키 설정
echo "PORT=5000\nOPENWEATHERMAP_API_KEY=your_api_key_here" > .env

# 개발 서버 실행
npm run dev
```

백엔드 서버는 http://localhost:5000 에서 실행됩니다.

## 📊 CI/CD 파이프라인

이 프로젝트는 GitHub Actions를 사용하여 자동화된 CI/CD 파이프라인을 구현했습니다:

### 프론트엔드 파이프라인 (`frontend-ci.yml`)

```yaml
# 주요 단계
- 코드 체크아웃
- Node.js 설정
- 의존성 설치
- 린트 검사
- 테스트 실행
- 프로젝트 빌드
- GitHub Pages에 배포
```

### 백엔드 파이프라인 (`backend-ci.yml`)

```yaml
# 주요 단계
- 코드 체크아웃
- Node.js 설정
- 의존성 설치
- 린트 검사
- 테스트 실행
- Heroku에 배포
```

## 🧪 테스트

### 프론트엔드 테스트

```bash
cd frontend
npm test
```

### 백엔드 테스트

```bash
cd backend
npm test
```

## 🔍 API 엔드포인트

### 현재 날씨

- `GET /api/weather/city/:city` - 도시 이름으로 현재 날씨 조회
- `GET /api/weather/coordinates?lat=<latitude>&lon=<longitude>` - 좌표로 현재 날씨 조회

### 날씨 예보

- `GET /api/forecast/city/:city` - 도시 이름으로 5일 예보 조회
- `GET /api/forecast/coordinates?lat=<latitude>&lon=<longitude>` - 좌표로 5일 예보 조회

## 🌩️ GitHub Actions 실습 가이드

1. **저장소 포크 또는 클론**
   - 이 저장소를 자신의 GitHub 계정으로 포크하거나 클론합니다.

2. **GitHub Secrets 설정**
   - GitHub 저장소 설정 → Secrets and Variables → Actions에서 다음 시크릿을 추가합니다:
     - `OPENWEATHERMAP_API_KEY` - OpenWeatherMap API 키
     - `HEROKU_API_KEY` - Heroku API 키 (Heroku 배포 시 필요)
     - `HEROKU_APP_NAME` - Heroku 앱 이름 (Heroku 배포 시 필요)
     - `HEROKU_EMAIL` - Heroku 계정 이메일 (Heroku 배포 시 필요)

3. **워크플로우 파일 수정**
   - `.github/workflows/frontend-ci.yml`과 `.github/workflows/backend-ci.yml` 파일을 필요에 따라 수정합니다.

4. **테스트 워크플로우 실행**
   - 코드를 수정하고 커밋하여 자동화된 워크플로우가 실행되는지 확인합니다.
   - GitHub Actions 탭에서 워크플로우 실행 상태를 모니터링합니다.

5. **추가 도전 과제**
   - 테스트 커버리지 리포트 생성 및 배포
   - SonarCloud 연동 코드 품질 검사
   - Docker 컨테이너 빌드 및 배포
   - 슬랙/디스코드 알림 통합
   - 다중 환경(개발, 스테이징, 프로덕션) 배포 파이프라인 구성

## 📝 학습 목표

- GitHub Actions의 기본 개념 이해
- CI/CD 파이프라인 구축 및 구성 방법 학습
- 자동화된 테스트와 배포의 중요성 이해
- 실제 프로젝트에 적용 가능한 CI/CD 패턴 습득

## 📚 참고 자료

- [GitHub Actions 공식 문서](https://docs.github.com/en/actions)
- [React 공식 문서](https://reactjs.org/)
- [Express 공식 문서](https://expressjs.com/)
- [OpenWeatherMap API 문서](https://openweathermap.org/api)
- [Heroku 배포 가이드](https://devcenter.heroku.com/categories/deployment)

## 🔄 기여 방법

1. 저장소를 포크합니다.
2. 새 브랜치를 생성합니다: `git checkout -b my-feature-branch`
3. 변경 사항을 커밋합니다: `git commit -m 'Add some feature'`
4. 포크한 저장소에 푸시합니다: `git push origin my-feature-branch`
5. Pull Request를 제출합니다.

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

<div align="center">
  <p>이 프로젝트는 융합해커톤을 위한 GitHub Actions CI/CD 실습 자료입니다.</p>
  <p>© 2023 Weather Wizard Team</p>
</div>
