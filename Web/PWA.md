# PWA(Progressive Web App)

웹과 네이티브 앱의 장점을 결합한 웹앱

## 핵심 기술

- 서비스 워커(Service Worker)
  - 백그라운드에서 네트워크 요청을 관리하는 스크립트
  - 캐시 저장하여 오프라인 지원 & 빠른 로딩 가능
- 웹 앱 매니페스트(Web App Manifest)
  - PWA가 설치될 때 앱의 이름, 아이콘, 색상 등을 설정하는 파일(manifest.json)

```
{
   "name": "My PWA App",
   "short_name": "PWA",
   "start_url": "/index.html",
   "icons": [
     {
       "src": "/icons/icon-192x192.png",
       "sizes": "192x192",
       "type": "image/png"
     }
   ],
   "display": "standalone"
}
```

## 장점

### 설치 없이 바로 사용 가능

- 브라우저에서 열면 바로 앱처럼 사용 가능
- App Store 없이 URL만 공유하면 됨

### 홈화면에 앱처럼 설치 가능

- 아이콘을 홈화면에 추가할 수 있어 네이티브 앱처럼 실행

### 오프라인 지원

- Service Worker가 캐시를 관리해서 네트워크 없이도 사용 가능

### 푸시 알림 지원

- Android에서는 웹 푸시 알림을 지원해 사용자 리텐션 향상 가능

### 속도 개선

- 필요한 자원만 캐싱하여 재방문 시 로딩이 매우 빠름

### 다양한 플랫폼 호환

- iOS, Android, 데스크탑 등에서 동일 코드로 작동

## 단점

### iOS 기능 제한

- 푸시 알림은 iOS 16.4부터 지원하지만, 제한 많고 조건도 복잡
- 백그라운드 동작이나 스토리지 사용량에도 제약

### 브라우저 종속

- 사용자가 PWA를 인지하고 직접 설치해야 함(자동 설치 X)
- 브라우저마다 기능 지원 수준이 다름

### 앱스토어 진입 불가(기본적으론)

- 일반적인 방식으로는 Apple App Store/Google Play에 등록 어려움
- 단, TWA(Trusted Web Activity)로 안드로이드 등록 가능

### 보안 위험 요소 관리 필요

- Service Worker는 네트워크 캐시, 요청 가로채기 등 민감한 작업을 하므로 보안 이슈에 주의 필요

### 네이티브 기능 제한

- BLE, NFC, 생체인증, 고급 카메라 기능 등은 일부 또는 미지원
