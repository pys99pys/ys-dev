# Dockerfile과 docker-compose

| 항목 | Dockerfile | docker-compose |
|------|-------------|------------------|
| 역할 | 컨테이너 이미지 생성 정의 | 여러 컨테이너를 동시에 구성 및 실행 |
| 사용 파일 | `Dockerfile` | `docker-compose.yml` |
| 사용 명령어 | `docker build`, `docker run` | `docker-compose up`, `docker-compose down` |
| 주요 용도 | 애플리케이션 이미지 만들기 | 앱 + DB + Redis 같은 서비스 묶음 실행 |
| 단일/다중 컨테이너 | 보통 단일 컨테이너 | 여러 컨테이너 연결 (서비스 단위) |
| 실행 속도 | 개별 실행 | 한 번에 전부 실행 가능 |
| 파일 위치 | 각 프로젝트 내에 위치 | 루트 또는 devops 디렉토리에 위치 |
