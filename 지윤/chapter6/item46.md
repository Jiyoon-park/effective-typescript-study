#### 아이템46. 타입 선언과 관련된 세 가지 버전 이해하기

타입스크립트를 사용하면 신경쓸 라이브러리 버전들이 늘어나 의존성 관리가 더 어려워진다.

- 라이브러리 버전
- 타입 선언(@types) 버전
- 타입스크립트의 버전

일반적으로 라이브러리는 dependencies / 타입 정보 라이브러리는 devDependencies에 설치한다.

라이브러리가 semver 규칙을 지킨다는 전제 하에, 라이브러리와 타입라이브러리의 버전은 메이저와 마이너 버전은 일치하되 패치 버전은 일치하지 않을 수 있다. (패치 버전 업데이트는 API 사양을 변경하지 않으므로)

이렇게 라이브러리와 타입라이브러리의 버전을 따로 관리하는 것은 아래와 같은 문제 상황이 생길 수 있다.

1. 라이브러리는 업데이트, 타입 라이브러리는 업데이트 안함

   - 타입 오류 발생
   - interface를 보강하면 라이브러리에 업데이트된 기능 사용 가능

2. 라이브러리는 안 업데이트, 타입 라이브러리는 업데이트

   - 라이브러리의 버전을 올리거나, 타입 라이브러리의 버전을 내리면 사용 가능

3. 프로젝트 타입스크립트 버전보다 라이브러리에서 요구하는 타입스크립트 버전이 더 최신 버전

   - 프로젝트 타입스크립트 버전을 올리거나, 라이브러리 타입 선언의 버전을 내리면 사용 가능

   - 또는 declare module 선언으로 라이브러리 타입 정보를 없애기

   - 라이브러리에서 typesVersions를 통해서 타입스크립트 버전별로 타입을 제공하기

     ```bash
     $ npm install --save-dev @types/lodash@ts3.1
     ```

4. @types 의존성 중복

   - 의존되는 @types의 버전을 서로 호환가능하도록 업데이트하기

라이브러리를 공개하려는 경우, 타입스크립트로 작성된 라이브러리라면, 타입 선언을 자체적으로 포함시키는 것이 좋고, 자바스크립트로 작성된 라이브러리라면, DefinitelyTyped에 타입 선언을 따로 공개하는 것이 좋다.
