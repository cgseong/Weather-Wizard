# Weather Wizard Frontend

<div align="center">
  <img src="https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB">
  <img src="https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E">
  <img src="https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white">
</div>

Weather Wizard의 프론트엔드 애플리케이션입니다. 이 애플리케이션은 React로 개발되었으며, 사용자에게 현재 날씨 정보와 5일 예보를 제공합니다.

## 기능

- 현재 위치 기반 날씨 정보 표시
- 도시 검색 기능
- 실시간 날씨 상세 정보 (온도, 습도, 풍속 등)
- 5일 날씨 예보
- 반응형 디자인 (모바일 및 데스크톱 지원)

## 기술 스택

- **React**: 사용자 인터페이스 구축
- **React Router**: 페이지 라우팅
- **Axios**: API 요청 처리
- **React Icons**: 아이콘 컴포넌트
- **Jest & React Testing Library**: 테스트
- **GitHub Actions**: CI/CD 파이프라인

## 설치 및 실행

### 요구사항

- Node.js 14.x 이상
- npm 6.x 이상

### 설치

```bash
# 의존성 설치
npm install
```

### 개발 서버 실행

```bash
npm start
```

브라우저에서 http://localhost:3000 에 접속하여 애플리케이션을 확인할 수 있습니다.

### 프로덕션 빌드

```bash
npm run build
```

빌드된 파일은 `build` 디렉토리에 생성됩니다.

## 프로젝트 구조

```
src/
├── components/         # 재사용 가능한 컴포넌트
│   ├── Alert.js        # 알림 메시지 컴포넌트
│   ├── Header.js       # 헤더 컴포넌트
│   ├── Footer.js       # 푸터 컴포넌트
│   ├── SearchBar.js    # 도시 검색 컴포넌트
│   ├── WeatherCard.js  # 날씨 정보 카드 컴포넌트
│   └── ForecastCard.js # 예보 카드 컴포넌트
├── pages/              # 페이지 컴포넌트
│   ├── Home.js         # 메인 페이지 (현재 날씨)
│   ├── Forecast.js     # 5일 예보 페이지
│   └── About.js        # 소개 페이지
├── services/           # API 서비스
│   └── weatherService.js # 날씨 API 통신 서비스
├── styles/             # CSS 스타일
│   ├── global.css      # 전역 스타일
│   ├── Header.css      # 헤더 스타일
│   └── ... (컴포넌트별 스타일)
├── __tests__/          # 테스트 파일
│   ├── WeatherCard.test.js
│   ├── SearchBar.test.js
│   └── ...
├── App.js              # 메인 App 컴포넌트
└── index.js            # 진입점
```

## 주요 컴포넌트

### SearchBar

도시 이름을 입력받아 날씨 검색 기능을 제공합니다.

```jsx
<SearchBar onSearch={handleSearch} />
```

### WeatherCard

현재 날씨 정보를 시각적으로 표시합니다.

```jsx
<WeatherCard data={weatherData} />
```

### ForecastCard

예보 데이터를 카드 형태로 표시합니다.

```jsx
<ForecastCard data={forecastItem} />
```

## API 통신

백엔드 API와의 통신은 `services/weatherService.js`에서 처리합니다:

```javascript
// 도시별 날씨 조회
const weatherData = await weatherService.getWeatherByCity(city);

// 좌표별 날씨 조회
const weatherData = await weatherService.getWeatherByCoordinates(latitude, longitude);

// 5일 예보 조회
const forecastData = await weatherService.getForecastByCity(city);
```

## 환경 변수

`.env.development` 또는 `.env.production` 파일에서 환경 변수를 설정합니다:

```
REACT_APP_API_BASE_URL=http://localhost:5000/api  # 개발 환경
REACT_APP_API_BASE_URL=https://your-backend-app.herokuapp.com/api  # 프로덕션 환경
```

## 테스트

Jest와 React Testing Library를 사용하여 컴포넌트를 테스트합니다.

```bash
# 모든 테스트 실행
npm test

# 특정 파일만 테스트
npm test -- WeatherCard.test.js

# 커버리지 보고서 생성
npm test -- --coverage
```

## CI/CD 파이프라인

GitHub Actions를 사용한 CI/CD 파이프라인이 구성되어 있습니다:

- 코드 푸시 및 PR 시 자동 테스트 실행
- 린트 검사로 코드 품질 확인
- 테스트 통과 시 자동 빌드
- main 브랜치 병합 시 GitHub Pages에 자동 배포

CI/CD 설정은 `.github/workflows/frontend-ci.yml` 파일에서 확인할 수 있습니다.

## 배포

`main` 브랜치에 코드가 병합되면 GitHub Actions를 통해 GitHub Pages에 자동으로 배포됩니다:

```
https://{github-username}.github.io/weather-wizard/
```

## 스크린샷

### 홈 화면
![홈 화면](screenshots/home.png)

### 예보 화면
![예보 화면](screenshots/forecast.png)

## 문제 해결

**API 연결 오류가 발생하는 경우:**
1. 백엔드 서버가 실행 중인지 확인하세요.
2. `.env` 파일의 `REACT_APP_API_BASE_URL` 설정이 올바른지 확인하세요.
3. 네트워크 요청 시 CORS 오류가 없는지 확인하세요.

**위치 정보를 가져올 수 없는 경우:**
1. 브라우저에서 위치 정보 접근 권한이 허용되어 있는지 확인하세요.
2. HTTPS 환경에서 실행 중인지 확인하세요 (위치 정보는 보안 연결에서만 작동합니다).

## 참고 자료

- [React 공식 문서](https://reactjs.org/)
- [Create React App 가이드](https://create-react-app.dev/)
- [OpenWeatherMap API 문서](https://openweathermap.org/api)
- [GitHub Actions 문서](https://docs.github.com/en/actions)

---

이 프로젝트는 GitHub Actions CI/CD 파이프라인 구축 실습을 위한 토이 프로젝트입니다.
