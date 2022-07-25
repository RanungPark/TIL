DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API 즉 프로퍼티와 메서드를 제공하는 트리 자료구조다

HTML 요소 간에 중첩 관계에 의해 계층적인 부자 관계가 형성된다 이러한 HTML 요소 간의 부자 관계를 반영하여 HTML 문서의 구성요소인 HTML 요소를 객체화한 모든 노드 객체들의 트리 구조로 구성한다

노드 객체는 종류가 있고 상속 구조를 갖는다

문서노드는 DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다 document 객체는 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체로서 전역 객체 window의 document 프로퍼티에 바인딩되어 있다 따라서 문서노드는 window.document또는 document로 참조할 수 있다

document 객체는 DOM 트리의 루트 노드이므로 DOM 트리의 노드들에 접근하기 위한 진입점 역할을 담당한다 즉 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다

요소 노드는 HTML  요소를 가리키는 객체다 요소노드는 HTML 요소 간의 중첩에 의해 부자 관계를 가지며 이 부자 관계를 통해 정보를 구조화한다 즉 문서의 구조를 표현한다

어트리뷰트 노드는 HTML 요소의 어트리부트를 가리키는 객체다 어트리뷰트 노드는 어트리뷰트가 지정된 HTML 요소의 요소에만 연결되어 있다 따라서 어트리뷰트 노드에 접근하려 어트리뷰트를 참조하거나 변경하려면 먼저 요소 노드에 접근해야 한다

텍스트 노드는 HTML 요소의 텍스트를 가리키는 객체다 텍스트 노드는 요소 노드의 자식이며 자식을 가질 수 없는 리프 노드다 따라서 텍스트 노드에 접근하려면 부모노드인 요소 노드에 접근 해야한다

DOM API를 이용하여 노드 객체는 자신의 부모, 형제, 자식을 탐색할 수 있으며 어트리뷰트와 텍스트를 조작할 수도 있다

DOM을 구성하는 객체는 브라우저 환경에서 추가적으로 제공하는 호스트 객체이다

자바스크립트 객체이브로 프로토타입의 상속구조를 갖는다(Object - EventTarget - Node를 상속받는다)

DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공한다 이 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다

---

getElementById 메서드는 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드를 탐색하여 반환한다 중복된 id 값이 존재하면 첫 번째 요소 노드만 반환하며 존재하지 않으면 null을 반환한다

암묵적으로 id값과 동일한 이름의 전역 변수가 선언되며 전역 변수가 이미 선언되어 있으면 변수에 노드 객체가 재할당되지 않는다

getElementsByTagName 메서드는 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환한다 이 메서드가 반환하는 객체는 유사 배열이면서 이터러블이다

getElementsByClassName 메서드는 인수로 전달한 class 어트리뷰트을 갖는 모든 요소 노드들을 탐색하여 반환한다

공백으로 구분하여 여러개의 class를 지정할 수 있다

querySelector 메서드는 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 탐색하여 반환한다

querySelectorAll 메서드는 CSS 선택자를 만족시키는 모든 요소 노드를 탐색하여 반환한다

getElementsByTagName , getElementsByClassName, querySelector, querySelectorAll   는 Element.prototype으로 특정 요소 노드를 통해 호출하면 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환한다

querySelector는 getElement***보다 느리지만 일관된 방식으로 요소 노드를 취득할 수 있다는 장점이 있다 따라서 id 속성이 있는 노드를 취득할때만 getElementById 을 사용하고 그외에는 querySelector, querySelectorAll 을 사용하는 것을 권장한다

getElementsBy*** 은 HTMLCollection을 반환한다 이는 살아있는 객체라고도 불리는데 상태의 변화를 실시간으로 반영하기 때문에 for문을 순회할때 오류가 발생할 가능성이 있다 이는 고차함수를 사용하거나 querySelectorAll를 사용하여 해결할 수 있는데 querySelectorAll은 NodeList 객체를 반환한다 이는 실시간으로 상태 변경을 반영하지 않는다 하지만 childNodes 프로퍼티가 반환하는 NodeList 객체는 HTMLCollection 객체와 같이 실시간으로 노드 객체의 상태를 변경을 반영하는 live 객체로 동작하므로 주의가 필요하다

따라서 노드 객체의 상태 변경과 상관없이 DOM 컬렉션을 안전하게 사용하려면 NodeList ,HTMLCollection 객체를 배열로 만드는 것이다 이 두 객체는 이터러블이므로 스프레드 문법으로 간편하게 배열로 바꿀수 있다

textContent 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이) 내의 텍스트 모두 반환한다HTML 마크업은 무시된다

innerHTML 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역 내에 포함된 모든 HTML 마크업을 문자열로 반환한다

innerHTML 할당한 문자열에 포함되어 있는 HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영된다(textContent는 HTML 마크업이 파싱되지 않는다)

innerHTML은 크로스 사이트 스크립팅 공격에 취약한 단점이 있다

요소 노드 생성 Document.prototype.createElement(tageName)

텍스트 노드 생성 Document.prototype.createTextNode(text)

텍스트 노드를 요소 노드의 자식 노드로 추가 Node.prototype.appendChild(childNode) (마지막 자식 요소에 추가한다)

여러 개의 요소를 DOM에 추가하는 경우 DocumentFragment 노드를 사용하는 것이 효율적이다

createDocumentFragment를 생성하여 여러게의 요소를 fragement에 넣고 fragment를 DOM요소에 추가한다

노드 삽입

appendChild는 마지막 자식 노드로 추가한다

사용자 입력에 의한 상태 변화와 관계있는 DOM 프로퍼티만 최신 상태 값을 관리한다 그 외의 사용자 입력에 의한 상태 변화와 관계없는 어트리뷰트와 DOM 프로퍼티는 항상 동일한 값으로 연동한다

HTML 어트리뷰트로 지정한 HTML 요소의 초기상태는 어트리뷰트 노드에서 관리한다

getAttribute(HTML 어트리뷰트) 메서드로 취득한 어트리뷰트 값은 언제나 문자열이다 하지만 DOM 프로퍼티로 취득한 최신 상태 값은 문자열이 아닐 수도 있다

인라인 스타일 변경은 HTMLElement.prototype.style 프로퍼티로 취득하거나 추가 변경 한다