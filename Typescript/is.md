타입 가드를 이용하여 특정 타입을 보장하고 싶을 때 사용한다.

```javascript
const isString = (target: unknown): target is string => {
  return typeof target === "string";
};

const isNumber = (target: unknown): target is number => {
  return typeof target === "number";
};

const test = (target: unknown) => {
  if (isString(target)) {
    console.log(target.toUpperCase());
  }

  if (isNumber(target)) {
    console.log(target + 1);
  }
};

test("message!"); // MESSAGE!
test(99); // 100
```

타입 가드에 의해 타입이 보장되므로 `as` 키워드로 타입 단언을 하지 않아도 된다.
