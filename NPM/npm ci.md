## package.json과 package-lock.json

npm install은 특정 파일과 밀접한 관계가 있다.

- package.json
- package-lock.json

**package.json**은 설치하고자 하는 의존성 모듈에 대한 목록이 있으며, 의존성 목록의 버전은 [semver](https://docs.npmjs.com/cli/v6/using-npm/semver)를 따른다.

```javascript
"react": "^17.0.2",
```

version range로 인해 각자 서로 다른 버전의 node_modules를 생성할 수 있다는 문제가 있다.

예를 들어, 서로 다른 환경에서 개발중인 개발자가 각자의 환경에서 npm install을 실행하면 서로 다른 버전의 모듈이 node_modules에 설치될 수 있다.

그래서 **package-lock.json**이 존재한다. **package-lock.json**은 **package.json**과는 다르게 정확한 버전이 명시되어 있다.

```javascript
react@^17.0.2:
  version "17.0.2"
```

따라서 서로 다른 환경의 개발자도 **pacakage-lock.json**을 공유한다면 같은 버전의 의존성 모듈을 설치할 수 있다.

## npm install

두 명령어 모두 결과적으로 의존성 모듈을 설치해주는 명령어이다. `npm install`의 본질은 다음과 같다.

> package.json 을 읽어 의존성 목록을 만들고 package-lock.json 을 통해 설치할 의존성의 버전을 알려주는 것

`npm install`을 실행하면 **package.json**에 의존성이 추가되고, **package-lock.json**도 업데이트 된다. 즉, `npm install` 명령어는 **package.json**과 **package-lock.json**에 쓰기 권한을 가진다.

## npm ci

`npm ci` 명령어의 특징은 다음과 같다.

- **package-lock.json**이 무조건 존재해야 하고, 없으면 에러를 낸다.
- **package-lock.json**을 기반으로 의존성 모듈을 설치하고, **package.json**은 버전 매칭 밸리데이션 용도로 사용한다. 즉, **package-lock.json**과 **package.json** 사이의 버전이 매칭이 안되면 에러를 낸다.
- `npm ci`를 실행하면 먼저 node_modules 삭제한 후, 의존성 모듈을 한번에 설치한다.

이처럼 `npm install` 명령어와 달리 **package.json**과 **package-lock.json**을 수정하지 않기 때문에 쓰기 권한을 가지지 않는다.

## npm install vs npm ci

`npm ci`는 버전이 명확하게 명시된 **package-lock.json**을 기반으로 설치하기 때문에 설치할 버전을 알아내야 하는 `npm install`보다 빠르다고 알려져 있다.

하지만 `npm ci`는 node_modules를 삭제하기 때문에 node_modules를 삭제하는 연산이 길어진다면 `npm install`보다 느린 경우가 생길수도 있다.

개발 환경이 아닌 CI 환경에서는 **package-lock.json**을 기반으로 명확한 버전을 설치하는 `npm ci`가 더 적합한 방법으로 여겨진다.

## yarn에서는?

yarn에서도 `npm ci`와 같은 기능을 제공하고 있다.

```
yarn install --frozen-lockfile
```

위 명령어는 deprecate될 예정이고, 아래 명령어로 대체된다고 한다.

```
yarn install --immutable --immutable-cache --check-cache
```
