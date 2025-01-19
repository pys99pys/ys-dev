# requestAnimationFrame

브라우저가 애니메이션을 더 효율적으로 처리할 수 있도록 제공하는 JavaScript 함수

애니메이션을 실행할 콜백을 등록하며, 브라우저의 화면 새로 고침 주기(주로 60fps, 약 16.7ms 간격)에 맞춰 콜백을 실행

## 특징

### 효율적 업데이트

- setInterval이나 setTimeout을 사용할 때보다 더 적절한 시점에 애니메이션을 업데이트하여 CPU/GPU 사용을 최적화
- 브라우저가 비활성 탭일 경우 실행을 중단하여 리소스를 절약

### 프레임 동기화

- 브라우저의 화면 재렌더링 주기에 맞춰 콜백이 실행되어 부드러운 애니메이션을 보장

### 사용 사례

- CSS를 JavaScript로 제어하는 애니메이션
- 게임 개발에서 프레임 업데이트
- 스크롤 이벤트와 같이 동적인 효과를 부드럽게 처리

## 사용법

### 기본 예제

```
function animate() {
  // 애니메이션 로직
  console.log('Frame rendered!');
  
  // 다음 프레임 예약
  requestAnimationFrame(animate);
}

// 애니메이션 시작
requestAnimationFrame(animate);
```

### 애니메이션 구현

**HTML**

```
<canvas id="canvas" width="500" height="500"></canvas>
```

**JavaScript**

```
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');

let x = 0;
let speed = 2;

function draw() {
  // 캔버스 지우기
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // 원 그리기
  ctx.beginPath();
  ctx.arc(x, canvas.height / 2, 20, 0, Math.PI * 2);
  ctx.fillStyle = 'blue';
  ctx.fill();

  // 위치 업데이트
  x += speed;
  if (x > canvas.width || x < 0) {
    speed *= -1; // 벽에 닿으면 방향 전환
  }

  // 다음 프레임 예약
  requestAnimationFrame(draw);
}

// 애니메이션 시작
draw();
```

### 정지 및 시작 제어

requestAnimationFrame은 정지 기능이 내장되어 있지 않으므로, 구현하려면 cancelAnimationFrame()을 사용해야 함

```
let animationId;

function startAnimation() {
  function animate() {
    console.log('Animating...');
    animationId = requestAnimationFrame(animate);
  }
  animate();
}

function stopAnimation() {
  cancelAnimationFrame(animationId);
}

// 애니메이션 시작
startAnimation();

// 일정 시간 후 애니메이션 정지
setTimeout(stopAnimation, 5000);
```

## vs setTimeout

### 호출 주기

- setTimeout: 고정된 주기 (예: 16ms)
- requestAnimationFrame: 화면 재렌더링 주기 (대개 16.7ms)

### 효율성

- setTimeout: 비효율적(비활성 탭에서도 실행)
- requestAnimationFrame: 비활성 탭에서는 실행 중단(리소스 절약)

### 부드러운 애니메이션

- setTimeout: 덜 부드러움
- requestAnimationFrame: 더 부드러움
