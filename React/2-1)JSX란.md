# 2. 리액트 핵심 요소 깊게 살표보기(2-1)

## 2-1 JSX란?

JSX는 XML과 유사한 내장형 구문이며 리액트에 종속적이지 않은 독자적인 문법으로 보는 것이 옳다.

리액트에서 독자적으로 개발했다는 사실에서 미루어 알 수 있듯이 JSX는 ECAMScript의 표준이 아니다. 즉 자바스크립트 엔진이나 브라우저에 의해서 실행되거나 표현되도록 만들어진 구문이 아니다

그렇기 때문에 JSX는 반드시 트랜스 파일러를 거쳐야 비소로 자바스크립트 런타임이 이해할 수 있는 의미 있는 자바스크립트 코드로 변환된다.

JSX의 설계 목적은 JSX 내부에 트리 구조로 표현하고 싶은 다양한 것들을 작성해 두고, 이 JSX를 트랜스파일이라는 고정을 거쳐 자바스크립트가 이해할 수 있는 코드로 변경하는 것이 목표이다

### JSX의 정의

**JSXElement**

JSX를 구성하는 가장 기본 요소로, HTML의 요소와 비슷한 역할을 한다.

사용자가 컴포넌트를 만들어 사용할 때에는 반드시 대문자로 시작하는 컴포넌트를 만들어야만 사용 가능하다. 이유는 컴포넌트 태그명을 구분 짓기 위해서다

**JSXAttributes**

JSXElement에 부여할 수 있는 속성을 의미한다. 필수 값이 아니고 존재하지 않아도 에러가 나지는 않는다.

**JSXChildren**

JSXEelemt의 자식 값을 나타낸다. JSX는 앞서 언급했듯 속성을 가진 트리 구조를 나타내기 위해 만들어 졌기 때문에 JSX로 부모와 자식 관계를 나타낼 수 있으며, 그 자식을 JSXChildren이라고 한다.

**JSXString**

HTML과 JSX 사이에 복사와 붙여넣기를 쉽게 할 수 있도록 설계돼 있다. HTML에서 사용 가능한 문자열은 모두 JSXString에서도 사용이 가능하다

“큰따옴표로 구성된 문자열”, ‘작은따옴표로 구성된 문자열’ 혹은 JSXText가 여기에 속한다

자바스크립트와는 가장 중요한 차이점인 이스케이프 문자를 허용하지 않는다. HTML과 유사하지 자바스크립트에서 지원하는 이스케이프는 허용하지 않는다.

JSX는 HTML처럼 \을 이스케이프 문자열로 처리하고 있지 않다

### JSX 예제

- 처음 알게 된 예제

```jsx
const ComponentG = (
	<A>
		{/*옵션의 값으로 JSXElement를 넣는 것 또한 올바른 문법이다. */}
		<B optionalChildren = {<>안녕하세요</>}
	</A>
)
```

### JSX는 어떻게 자바스크립트에서 변환될까?

JSX를 변환하는 @babel/plugin-transform-react-jsx 플러그인을 알아야 한다.

바벨에서는 createElement를 이용하여 트랜스파일이 된다

- JSXElement를 첫 번째 인수로 선언해 요소를 정의한다.
- 옵셔널인 JSXChildren, JSXAttributes, JSXString는 이후 인수로 넘겨주어 처리한다.

```jsx
function TextOrHeading({
	isHeading,
	children,
}: PropsWithChildren<{ isHeading: boolean }>) {
	return isHeading ? (
		<h1 className="text">{children}</h1>
	) : (
		<span className="text">{children}</h1>
	)
}
```

```jsx
import { createElement } from 'react'

function TextOrHeading({
	isHeading,
	children,
}: PropsWithChildren<{ isHeading: boolean }>) {
	return createElement(
		isHeading ? 'h1' : 'span',
		{ className: 'text' },
		children,
	)
}
```

이처럼 JSXElement만 다르고 옵셔널인 요소들이 동일한 상황에서 최소화 할 수 있다.

JSX 반환값이 결국 React.createElement로 귀결된다는 사실을 파악한다면 위와 같은 방식으로 리팩터링 할 수 있다.

### 정리

JSX 내부에 자바스크립트 문법이 많아질수록 복잡성이 증대하면서 코드의 가독성도 해칠 것이므로 주의해서 사용해야한다.

리액트 내부에서 JSX가 어떻게 변환되는지 어떤 결과물을 만들어내는지 알아두면 향후에 리액트 애플리케이션을 만드는데 도움이 될 수 있다.