# esbuild

매우 빠른 JavaScript 및 TypeScript 번들러로 특히 빌드 속도와 간결한 설정을 중점적으로 설계된 도구

Go 언어로 작성되어 동시성을 극대화했고, 번들링, 트랜스파일링, 축소화(minification) 등을 빠르게 처리할 수 있음

## 특징

- 빠른 속도
  - Go 언어의 효율성과 멀티스레딩을 활용해 동작하기 때문에 빌드 속도가 매우 빠름
  - 기존의 JavaScript 기반 번들러(Webpack, Rollup 등)보다 최대 100배 빠름
- TypeScript와 JSX 지원
  - TypeScript 및 JSX를 별도 설정 없이도 기본 지원
- 간단한 설정
  - 복잡한 설정 파일 없이 간단한 CLI 명령이나 API로 작동 가능
- 트리 쉐이킹(Tree Shaking)
  - 사용하지 않는 코드를 자동으로 제거하여 번들 크기를 최소화
- ESM 및 CommonJS 지원
  - ESM(ES Modules)과 CommonJS 모듈 시스템을 모두 지원
- CSS 및 이미지 번들링
  - CSS 파일과 정적 자산(이미지, 글꼴 등)도 처리 가능
 
## 주요 사용 사례

### 번들링(Bundling)

- 여러 JavaScript 및 TypeScript 파일을 하나의 파일로 묶어 제공

```
esbuild app.ts --bundle --outfile=out.js
```

### 트랜스파일링(Transpiling)

- TypeScript, 최신 JavaScript 문법을 이전 브라우저에서 호환되는 형태로 변환

```
esbuild app.ts --outfile=out.js --target=es6
```

### 압축(Minification)

- 코드를 축소하여 번들 크기를 줄임

```
esbuild app.ts --minify --outfile=out.js
```

### 개발 서버(Dev Server)

- 실시간 개발 서버로 사용할 수도 있음

```
esbuild app.ts --serve
```

### 코드 스플리팅(Code Splitting)

- 여러 파일을 나눠 필요한 부분만 로드하도록 번들링

```
esbuild entry1.ts entry2.ts --bundle --outdir=dist
```

## 장점

- 매우 빠른 빌드 속도: 멀티스레딩과 Go 언어 덕분에 대규모 프로젝트에서도 빠르게 동작
- 간편한 사용: 추가적인 설정 파일 없이도 CLI 명령으로 작업 가능
- 경량화: 필요 없는 코드를 제거하고, 최적화된 결과물을 제공
- 다양한 출력 옵션: CommonJS, ESM, UMD 등 다양한 모듈 형식 출력 가능

## 단점

- 플러그인 생태계 제한적: Webpack이나 Rollup과 비교하면 플러그인 생태계가 상대적으로 적음
- 고급 기능 부족: 커스텀 요구사항이 많은 복잡한 빌드 작업에는 제한적
- 구성 유연성 부족: 단순성과 속도에 초점이 맞춰져 있어 설정이 복잡한 프로젝트에는 적합하지 않을 수 있음
