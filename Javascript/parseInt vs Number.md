의미적으로 다름

- parseInt: 파싱, 진수 변환, 타입 변환
- Number: 타입 변환

```
parseInt("20px"); // 20
parseInt("10100", 2); // 20
parseInt("2e1"); // 2

Number("20px"); // NaN
Number("2e1"); // 20, 지수 표기법
```

- parseInt는 명시적 8진수를 감지하지 못하고 후행 문자를 무시
- Number는 명시적 8진수를 감지(암시적 8진수는 감지x)
  
```
parseInt("010"); // 10
parseInt('0o10'); // 0, o부터 무시됨

Number("010"); // 10
Number('0o10'); // 8
```

- 16진수 표기법은 둘 다 감지

```
parseInt("0xF"); //15
Number("0xF");   // 15
```
