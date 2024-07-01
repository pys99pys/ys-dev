# [2021-03-05] cloudFront Invalidation 권한 이슈

## 문제

github actions를 이용해서 cloudFront Invalidation을 하고자 했으나 Access Denined가 뜨면서 실패함

## 원인

해당 AWS 사용자가 cloudFront Invalidation을 할 권한이 없었음

## 해결

AWS Iam → 사용자 → 해당 사용자 → 권한 → 권한 추가 → CloudFrontFullAccess 추가
