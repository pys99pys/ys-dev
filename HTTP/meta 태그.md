# meta 태그

웹페이지의 정보를 정의하는 요소로, <head> 태그 내에서 설정됨

## 기본 메타 태그

### 문서 인코딩 설정

```
<meta charset="UTF-8">
```

- 웹페이지의 문자 인코딩을 설정
- UTF-8을 사용하면 다국어 지원 가능

### 뷰포트 설정(반응형 디자인)

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- 모바일 및 반응형 디자인을 위해 화면 크기를 설정
- width=device-width: 기기의 화면 너비에 맞춤
- initial-scale=1.0: 기본 확대 배율을 1로 설정.

### SEO 관련 메타 태그

```
<meta name="description" content="이 페이지는 HTML 메타데이터에 대한 설명을 제공합니다.">
<meta name="keywords" content="HTML, 메타데이터, SEO, 웹 개발">
<meta name="author" content="홍길동">
```

- description: 검색엔진에 표시될 페이지 설명(Google 검색결과에 표시됨)
- keywords: 검색엔진 최적화(SEO)용 키워드(하지만 현대 SEO에서는 영향이 적음)
- author: 페이지 작성자 정보

### 검색엔진 크롤링 설정

```
<meta name="robots" content="index, follow">
```

- index: 검색엔진이 페이지를 색인(index)하도록 허용
- follow: 검색엔진이 링크를 따라가도록 허용
- 검색엔진에 노출을 원하지 않는다면 noindex, nofollow 사용

## 소셜미디어 공유 최적화

### Open Graph(Facebook, 카카오톡)

```
<meta property="og:title" content="HTML 메타데이터란?">
<meta property="og:description" content="웹페이지의 정보를 정의하는 HTML 메타태그를 배워보세요.">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:url" content="https://example.com">
<meta property="og:type" content="website">
```

- og:title: 공유 시 표시될 제목
- og:description: 공유 시 표시될 설명
- og:image: 미리보기 이미지 (URL 형식)
- og:url: 페이지 URL
- og:type: 콘텐츠 유형(예: website, article, video 등)

### Twitter Card(트위터)

```
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="HTML 메타데이터란?">
<meta name="twitter:description" content="HTML 메타데이터에 대해 배워보세요.">
<meta name="twitter:image" content="https://example.com/image.jpg"
```

- twitter:card: 미리보기 스타일(summary, summary_large_image 등)
- twitter:title, twitter:description, twitter:image: Open Graph와 동일

### 기타 유용한 메타 태그

```
<meta http-equiv="refresh" content="5; url=https://example.com">
```

- 5초 후 example.com으로 자동 이동

### 테마 색상 (모바일 브라우저)

```
<meta name="theme-color" content="#ffffff">
```

- 모바일 브라우저에서 주소 표시줄 색상 변경 가능 (예: 크롬, 삼성 인터넷)

### iOS & 안드로이드 웹앱 설정

```
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="mobile-web-app-capable" content="yes">
```

- iOS 및 안드로이드에서 웹앱처럼 실행되도록 설정
