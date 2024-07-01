# Cloud Watch EC2 CPU 사용량 조회 쿼리

```
MAX(SEARCH('Namespace="AWS/EC2" MetricName="CPUUtilization" AutoScalingGroupName=my-app-*', 'Average', 60))
```
