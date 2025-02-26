# PWA

PWA(Progressive Web App)는 웹과 네이티브 앱의 장점을 결합한 웹앱

## 특징

- 설치 가능: 앱스토어 없이 홈 화면에 추가하여 앱처럼 사용 가능
- 오프라인 지원: 서비스 워커(Service Worker)를 이용해 네트워크 없이도 실행 가능
- 푸시 알림: 웹에서도 푸시 알림 제공(네이티브 앱과 유사한 UX)
- 빠른 로딩 속도: 캐시 저장으로 로딩 속도 향상
- 반응형 디자인: 모바일, 태블릿, PC 어디서든 최적화됨
- HTTPS 필요: 보안 강화를 위해 HTTPS 환경에서만 작동

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
