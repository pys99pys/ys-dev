## WebRTC(Web Real-Time Communication)

브라우저 간, 또는 브라우저와 네이티브 애플리케이션 간의 실시간 커뮤니케이션을 지원하는 기술

이를 통해 음성, 비디오, 데이터 공유를 가능하게 하며, 추가적인 플러그인이나 소프트웨어 없이 작동

## 주요 기능

- 실시간 음성/비디오 통신: 브라우저 간 실시간 음성 및 영상 스트리밍
- 데이터 전송: 브라우저 간 파일 및 데이터 전송
- P2P 연결: 중앙 서버 없이 브라우저 간 직접 연결

## 주요 구성 요소

### MediaStream

- 사용자의 카메라, 마이크 등 미디어 소스에 접근

```
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then((stream) => {
    // 미디어 스트림 처리
    const videoElement = document.querySelector("video");
    videoElement.srcObject = stream;
  })
  .catch((error) => {
    console.error("Error accessing media devices:", error);
  });
```

### RTCPeerConnection

- 브라우저 간 P2P 연결 설정
- 네트워크 정보를 교환 (SDP, ICE candidates)
- 미디어 및 데이터 스트림 전달

```
const peerConnection = new RTCPeerConnection();

// ICE Candidate 이벤트 처리
peerConnection.onicecandidate = (event) => {
  if (event.candidate) {
    console.log("New ICE candidate:", event.candidate);
  }
};

// 연결된 트랙 처리
peerConnection.ontrack = (event) => {
  const remoteStream = event.streams[0];
  const remoteVideo = document.querySelector("#remoteVideo");
  remoteVideo.srcObject = remoteStream;
};
```

### RTCDataChannel

- 브라우저 간 데이터 전송을 지원
- 주요 사용 사례: 파일 전송, 텍스트 메시지 교환

```
const dataChannel = peerConnection.createDataChannel("chat");

// 데이터 수신
dataChannel.onmessage = (event) => {
  console.log("Received data:", event.data);
};

// 데이터 전송
dataChannel.send("Hello, peer!");
```

## 작동 원리

브라우저 간 P2P 연결을 설정하여 데이터를 교환, 이 과정에는 몇 가지 중요한 단계가 있음

### SDP(Session Description Protocol)

- 연결에 대한 메타데이터(코덱, 해상도, 대역폭 등)를 교환.
- 브라우저 간 "Offer/Answer" 방식으로 진행.

### ICE (Interactive Connectivity Establishment)

- 네트워크 연결 가능성을 확인.
- P2P 연결을 설정하기 위해 사용 가능한 경로(TURN, STUN, Direct)를 탐색

### STUN/TURN 서버

- STUN 서버: 공용 IP 주소를 검색하고 NAT(Network Address Translation)를 우회
- TURN 서버: 직접 연결이 불가능할 경우 데이터를 중계

## 장점
- 실시간 통신: 낮은 지연 시간으로 음성, 영상, 데이터를 전송
- P2P 연결: 중앙 서버 비용 절감
- 브라우저 내장: 플러그인 불필요

## 단점
- NAT/Firewall 문제: 일부 네트워크 환경에서는 연결이 어려울 수 있음
- 복잡한 설정: STUN/TURN 서버 및 SDP 교환 과정
- 브라우저 지원 차이: 모든 브라우저에서 동일한 방식으로 동작하지 않을 수 있음.

## 주요 사용 사례

- 화상 회의: Zoom, Google Meet 등의 기술 기반
- 실시간 스트리밍: 게임, 스포츠 스트리밍
- 파일 공유: 피어 간 대용량 파일 전송
- 멀티플레이어 게임: 실시간 데이터 교환

## 시작하기

### 필수 서버 설정

- STUN/TURN 서버 설정
- WebSocket 서버를 통한 신호 교환(Signal Exchange)

### 예제

```
const configuration = { iceServers: [{ urls: "stun:stun.l.google.com:19302" }] };
const peerConnection = new RTCPeerConnection(configuration);

// 로컬 미디어 스트림 추가
navigator.mediaDevices.getUserMedia({ video: true, audio: true }).then((stream) => {
  stream.getTracks().forEach((track) => peerConnection.addTrack(track, stream));
});

// Offer 생성 및 설정
peerConnection.createOffer().then((offer) => {
  return peerConnection.setLocalDescription(offer);
});

// ICE Candidate 이벤트 처리
peerConnection.onicecandidate = (event) => {
  if (event.candidate) {
    console.log("ICE Candidate:", event.candidate);
  }
};

// 원격 스트림 처리
peerConnection.ontrack = (event) => {
  const remoteVideo = document.querySelector("#remoteVideo");
  remoteVideo.srcObject = event.streams[0];
};
```
