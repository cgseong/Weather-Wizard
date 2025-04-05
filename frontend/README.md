# Weather Wizard Frontend

<div align="center">
  <img src="https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB">
  <img src="https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E">
  <img src="https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white">
</div>

React로 개발된 Weather Wizard 애플리케이션의 프론트엔드 부분입니다. 이 애플리케이션은 사용자 위치 기반의 날씨 정보와 도시 검색을 통한 날씨 데이터를 제공합니다.

## 📋 목차

- [기능](#-기능)
- [기술 스택](#-기술-스택)
- [프로젝트 구조](#-프로젝트-구조)
- [시작하기](#-시작하기)
- [사용 가능한 스크립트](#-사용-가능한-스크립트)
- [환경 변수](#-환경-변수)
- [CI/CD 파이프라인](#-cicd-파이프라인)
- [테스트](#-테스트)
- [배포](#-배포)
- [참고 자료](#-참고-자료)

## 🌟 기능

- **현재 위치 날씨**: 사용자의 현재 위치를 기반으로 실시간 날씨 정보 제공
- **도시 검색**: 도시 이름으로 날씨 정보 검색
- **날씨 상세 정보**: 온도, 습도, 풍속, 기상 상태 등 상세 정보 표시
- **5일 예보**: 선택한 도시의 5일 날씨 예보 제공
- **반응형 디자인**: 모바일 및 데스크톱 환경에 최적화된 UI

## 🛠️ 기술 스택

- **React**: 사용자 인터페이스 구축
- **React Router**: 클라이언트 사이드 라우팅
- **Axios**: API 요청 처리
- **React Icons**: 아이콘 컴포넌트
- **CSS**: 컴포넌트 스타일링
- **Jest & React Testing Library**: 테스트

## 📁 프로젝트 구조

```
frontend/
├── public/                # 정적 파일
├── src/                   # 소스 코드
│   ├── components/        # 재사용 가능한 컴포넌트
│   │   ├── Alert.js
│   │   ├── Header.js
│   │   ├── Footer.js
│   │   ├── SearchBar.js
│   │   ├── WeatherCard.js
│   │   └── ForecastCard.js
│   ├── pages/             # 페이지 컴포넌트
│   │   ├── Home.js
│   │   ├── Forecast.js
│   │   └── About.js
│   ├── services/          # API 서비스
│   │   └── weatherService.js
│   ├── styles/            # CSS 스타일시트
│   │   ├── global.css
│   │   ├── Header.css
│   │   ├── WeatherCard.css
│   │   └── ...
│   ├── __tests__/         # 테스트 파일
│   │   ├── WeatherCard.test.js
│   │   ├── SearchBar.test.js
│   │   └── ...
│   ├── App.js             # 메인 App 컴포넌트
│   └── index.js           # 진입점
├── .github/
│   └── workflows/         # GitHub Actions 워크플로우
│       └── frontend-ci.yml
├── .env.development       # 개발 환경 변수
├── .env.production        # 프로덕션 환경 변수
├── package.json           # 프로젝트 의존성 및 스크립트
└── README.md              # 프론트엔드 문서
```

## 🚀 시작하기

### 사전 요구사항

- Node.js 14.x 이상
- npm 6.x 이상

### 설치

```bash
# 저장소 클론
git clone https://github.com/yourusername/weather-wizard.git
cd weather-wizard/frontend

# 의존성 설치
npm install
```

### 환경 설정

1. `.env.development` 파일이 있는지 확인하고 없으면 생성합니다:

```
REACT_APP_API_BASE_URL=http://localhost:5000/api
```

2. 백엔드 서버가 실행 중인지 확인합니다.

### 개발 서버 실행

```bash
npm start
```

브라우저에서 [http://localhost:3000](http://localhost:3000)으로 접속하여 애플리케이션을 확인할 수 있습니다.

## 📝 사용 가능한 스크립트

- **`npm start`**: 개발 서버 실행
- **`npm test`**: 테스트 실행
- **`npm run build`**: 프로덕션용 빌드 생성
- **`npm run lint`**: ESLint를 사용하여 코드 검사
- **`npm run format`**: Prettier를 사용하여 코드 포맷팅
- **`npm run test:coverage`**: 테스트 커버리지 리포트 생성

## 🔑 환경 변수

프로젝트에서 사용되는 환경 변수:

- **`REACT_APP_API_BASE_URL`**: 백엔드 API의 기본 URL
  - 개발 환경: `http://localhost:5000/api`
  - 프로덕션 환경: 배포된 백엔드 URL (예: `https://weather-wizard-api.herokuapp.com/api`)

## 🔄 CI/CD 파이프라인

이 프로젝트는 GitHub Actions를 사용하여 자동화된 CI/CD 파이프라인을 구현했습니다:

### 워크플로우 트리거

- **Push**: `main` 브랜치에 코드가 푸시될 때
- **Pull Request**: `main` 브랜치에 PR이 생성될 때
- 경로 필터: `frontend/**` (프론트엔드 코드가 변경된 경우에만)

### 워크플로우 단계

1. **코드 체크아웃**: 저장소 코드 가져오기
2. **Node.js 설정**: Node.js 환경 구성
3. **의존성 설치**: `npm ci`를 사용하여 의존성 설치
4. **린트 검사**: ESLint를 사용하여 코드 품질 검사
5. **테스트 실행**: Jest를 사용하여 테스트 실행
6. **프로젝트 빌드**: 프로덕션용 빌드 생성
7. **GitHub Pages 배포**: 빌드된 파일을 GitHub Pages에 배포 (main 브랜치 Push 시)

### 워크플로우 파일

```yaml
# .github/workflows/frontend-ci.yml
name: Frontend CI/CD

on:
  push:
    branches: [ main ]
    paths:
      - 'frontend/**'
  pull_request:
    branches: [ main ]
    paths:
      - 'frontend/**'

jobs:
  build_and_test:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./frontend
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
          cache: 'npm'
          cache-dependency-path: './frontend/package-lock.json'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Run tests
        run: npm test
      
      - name: Build project
        run: npm run build
      
      - name: Upload build artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-files
          path: frontend/build/

  deploy:
    needs: build_and_test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Download build artifacts
        uses: actions/download-artifact@v3
        with:
          name: build-files
          path: ./frontend/build
      
      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          folder: ./frontend/build
          branch: gh-pages
```

## 🧪 테스트

프로젝트는 Jest와 React Testing Library를 사용하여 테스트합니다.

### 테스트 실행

```bash
# 모든 테스트 실행
npm test

# 특정 테스트 파일 실행
npm test -- WeatherCard.test.js

# 테스트 커버리지 리포트 생성
npm test -- --coverage
```

### 주요 테스트 대상

- **컴포넌트 렌더링**: 컴포넌트가 올바르게 렌더링되는지 확인
- **사용자 상호작용**: 사용자 입력과 이벤트 처리 테스트
- **API 서비스**: API 호출 및 데이터 처리 로직 테스트

## 📦 배포

이 프로젝트는 GitHub Pages를 통해 자동으로 배포됩니다. 주요 배포 단계:

1. GitHub Actions 워크플로우가 트리거됩니다 (main 브랜치에 Push 시).
2. 코드 테스트 및 빌드가 성공적으로 완료됩니다.
3. 빌드된 파일이 gh-pages 브랜치에 배포됩니다.
4. 웹사이트는 `https://{github-username}.github.io/weather-wizard` 주소로 접근할 수 있습니다.

### 수동 배포

필요한 경우 수동으로 배포할 수 있습니다:

```bash
# 빌드 생성
npm run build

# GitHub Pages에 배포 (gh-pages 패키지 필요)
npm run deploy
```

## 📚 참고 자료

- [React 공식 문서](https://reactjs.org/)
- [Create React App 문서](https://create-react-app.dev/)
- [React Router 문서](https://reactrouter.com/)
- [Axios 문서](https://axios-http.com/)
- [GitHub Actions 문서](https://docs.github.com/en/actions)
- [OpenWeatherMap API 문서](https://openweathermap.org/api)

---

<div align="center">
  <p>이 프로젝트는 GitHub Actions CI/CD 파이프라인 구축 실습을 위한 토이 프로젝트입니다.</p>
  <p>© 2023 Weather Wizard Team</p>
</div>

