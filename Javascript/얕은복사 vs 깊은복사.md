## 얕은 복사(Shllow Copy)

원본과 복사한 값이 같은 참조를 가르키는것을 의미

### 1. Object.assign()

```
const obj = {
  a: 1,
  b: {
    c: 2,
  },
};

const copiedObj = Object.assign({}, obj);

copiedObj.b.c = 3

obj === copiedObj // false
obj.b.c === copiedObj.b.c // true
```

### 2. 전개연산자

```
const obj = {
  a: 1,
  b: {
    c: 2,
  },
};

const copiedObj = {...obj}

copiedObj.b.c = 3

obj === copiedObj // false
obj.b.c === copiedObj.b.c // true
```

## 깊은 복사(Deep Copy)

객체 안의 객체까지 원본과의 참조가 완전히 끊어진것을 의미

### 1. 재귀함수를 이용한 복사

### 2. JSON.stringify를 사용한 복사
