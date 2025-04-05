# Weather Wizard Backend

<div align="center">
  <img src="https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white">
  <img src="https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB">
  <img src="https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E">
  <img src="https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white">
</div>

Weather Wizard의 백엔드 API 서버입니다. 이 서버는 OpenWeatherMap API와 통신하여 날씨 데이터를 가져오고, 프론트엔드 애플리케이션에 제공합니다.

## 기능

- 도시 이름으로 현재 날씨 정보 제공
- 지리적 좌표(위도, 경도)로 현재 날씨 정보 제공
- 도시 이름으로 5일 날씨 예보 제공
- 지리적 좌표로 5일 날씨 예보 제공
- 에러 처리 및 로깅
- CORS 지원

## 기술 스택

- **Node.js**: 서버 환경
- **Express**: 웹 프레임워크
- **Axios**: HTTP 클라이언트
- **Jest & Supertest**: 테스트
- **GitHub Actions**: CI/CD 파이프라인
- **Heroku**: 클라우드 배포

## 설치 및 실행

### 요구사항

- Node.js 14.x 이상
- npm 6.x 이상
- OpenWeatherMap API 키 ([무료로 얻기](https://openweathermap.org/api))

### 설치

```bash
# 의존성 설치
npm install
```

### 환경 설정

루트 디렉토리에 `.env` 파일을 생성하고 다음 내용을 추가합니다:

```
PORT=5000
OPENWEATHERMAP_API_KEY=your_api_key_here
```

### 개발 서버 실행

```bash
# 개발 모드 (nodemon 사용)
npm run dev

# 프로덕션 모드
npm start
```

서버는 기본적으로 http://localhost:5000 에서 실행됩니다.

## API 엔드포인트

### 현재 날씨

- **GET** `/api/weather/city/:city`
  - 설명: 도시 이름으로 현재 날씨 정보를 가져옵니다.
  - 파라미터: `city` (도시 이름)
  - 응답 예시:
    ```json
    {
      "city": "Seoul",
      "temperature": 22,
      "condition": "맑음",
      "icon": "01d",
      "humidity": 65,
      "windSpeed": 3.5,
      "timestamp": "2023-06-10T12:00:00Z"
    }
    ```

- **GET** `/api/weather/coordinates`
  - 설명: 지리적 좌표로 현재 날씨 정보를 가져옵니다.
  - 쿼리 파라미터: `lat` (위도), `lon` (경도)
  - 요청 예시: `/api/weather/coordinates?lat=37.5665&lon=126.9780`
  - 응답 예시: 위와 동일

### 날씨 예보

- **GET** `/api/forecast/city/:city`
  - 설명: 도시 이름으로 5일 날씨 예보를 가져옵니다.
  - 파라미터: `city` (도시 이름)
  - 응답: 3시간 간격의 날씨 예보 배열

- **GET** `/api/forecast/coordinates`
  - 설명: 지리적 좌표로 5일 날씨 예보를 가져옵니다.
  - 쿼리 파라미터: `lat` (위도), `lon` (경도)
  - 요청 예시: `/api/forecast/coordinates?lat=37.5665&lon=126.9780`
  - 응답: 3시간 간격의 날씨 예보 배열

## 프로젝트 구조

```
src/
├── controllers/           # 요청 처리 컨트롤러
│   ├── weatherController.js  # 현재 날씨 관련 컨트롤러
│   └── forecastController.js # 예보 관련 컨트롤러
├── routes/                # API 라우트
│   ├── weather.js         # 날씨 라우트
│   └── forecast.js        # 예보 라우트
├── services/              # 외부 API 서비스
│   └── weatherService.js  # OpenWeatherMap API 연동
├── middleware/            # 미들웨어
│   └── errorHandler.js    # 에러 처리 미들웨어
├── utils/                 # 유틸리티 함수
│   └── logger.js          # 로깅 유틸리티
└── index.js               # 애플리케이션 진입점

tests/                     # 테스트 파일
├── weather.test.js        # 날씨 API 테스트
├── forecast.test.js       # 예보 API 테스트
└── weatherService.test.js # 날씨 서비스 테스트
```

## 서비스 구현

OpenWeatherMap API와의 통신은 `services/weatherService.js`에서 처리합니다:

```javascript
// src/services/weatherService.js (일부)

async function getWeatherByCity(city) {
  try {
    const response = await axios.get(`${BASE_URL}/weather`, {
      params: {
        q: city,
        appid: API_KEY,
        units: 'metric',
        lang: 'kr'
      }
    });
    
    // 응답 데이터 가공
    return {
      city: response.data.name,
      temperature: Math.round(response.data.main.temp),
      condition: response.data.weather[0].description,
      icon: response.data.weather[0].icon,
      humidity: response.data.main.humidity,
      windSpeed: response.data.wind.speed,
      timestamp: new Date(response.data.dt * 1000).toISOString()
    };
  } catch (error) {
    // 에러 처리
    console.error('날씨 데이터를 가져오는 중 오류 발생:', error.message);
    throw new Error(`날씨 데이터를 가져올 수 없습니다: ${error.message}`);
  }
}
```

## 테스트

Jest와 Supertest를 사용하여 API를 테스트합니다.

```bash
# 모든 테스트 실행
npm test

# 특정 파일만 테스트
npm test -- weather.test.js

# 커버리지 보고서 생성
npm run test:coverage
```

### 테스트 예시

```javascript
// tests/weather.test.js (일부)

test('GET /api/weather/city/:city should return weather data', async () => {
  // Mock data
  weatherService.getWeatherByCity.mockResolvedValue({
    city: 'Seoul',
    temperature: 22,
    condition: '맑음',
    icon: '01d',
    humidity: 65,
    windSpeed: 3.5
  });
  
  const res = await request(app)
    .get('/api/weather/city/Seoul')
    .expect('Content-Type', /json/)
    .expect(200);
  
  expect(res.body).toHaveProperty('city', 'Seoul');
  expect(res.body).toHaveProperty('temperature', 22);
});
```

## CI/CD 파이프라인

GitHub Actions를 사용한 CI/CD 파이프라인이 구성되어 있습니다:

- 코드 푸시 및 PR 시 자동 테스트 실행
- ESLint를 통한 코드 품질 검사
- 테스트 통과 시 자동 배포
- main 브랜치 병합 시 Heroku에 자동 배포

CI/CD 설정은 `.github/workflows/backend-ci.yml` 파일에서 확인할 수 있습니다.

```yaml
# .github/workflows/backend-ci.yml (주요 부분)
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
      - name: Install dependencies
        run: npm ci
      - name: Run linter
        run: npm run lint
      - name: Run tests
        run: npm test
        env:
          OPENWEATHERMAP_API_KEY: ${{ secrets.OPENWEATHERMAP_API_KEY }}

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Heroku
        uses: akhileshns/heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
          heroku_app_name: ${{ secrets.HEROKU_APP_NAME }}
          heroku_email: ${{ secrets.HEROKU_EMAIL }}
```

## 배포

### Heroku 배포

Heroku에 배포하기 위한 설정:

1. `Procfile` 파일 생성:
```
web: node src/index.js
```

2. 필요한 환경 변수 설정:
   - `OPENWEATHERMAP_API_KEY`: OpenWeatherMap API 키

3. GitHub Actions를 통한 자동 배포를 위해 GitHub 저장소에 Secrets 설정:
   - `HEROKU_API_KEY`
   - `HEROKU_APP_NAME`
   - `HEROKU_EMAIL`

### 수동 배포

```bash
# Heroku CLI가 설치되어 있어야 합니다
heroku login
heroku git:remote -a your-heroku-app-name
git push heroku main
```

## 에러 처리

API에서 반환되는 주요 에러 코드:

- **400** - 잘못된 요청 (필수 파라미터 누락)
- **404** - 리소스를 찾을 수 없음 (도시를 찾을 수 없음)
- **500** - 서버 내부 오류

에러 응답 형식:
```json
{
  "error": "에러 메시지"
}
```

## 성능 최적화

- 데이터 캐싱을 통한 외부 API 호출 최소화
- 응답 압축 (compression 미들웨어)
- CORS 설정 최적화
- 헬멧을 통한 보안 헤더 추가

## 로깅

중요한 이벤트와 에러는 콘솔에 로깅됩니다. 프로덕션 환경에서는 로깅 서비스 연동을 권장합니다.

## 참고 자료

- [Express 공식 문서](https://expressjs.com/)
- [OpenWeatherMap API 문서](https://openweathermap.org/api)
- [Jest 테스팅 프레임워크 문서](https://jestjs.io/)
- [GitHub Actions 문서](https://docs.github.com/en/actions)
- [Heroku 배포 가이드](https://devcenter.heroku.com/categories/deployment)

---

<div align="center">
  <p>이 프로젝트는 GitHub Actions CI/CD 파이프라인 구축 실습을 위한 토이 프로젝트입니다.</p>
  <p>© 2023 Weather Wizard Team</p>
</div>

