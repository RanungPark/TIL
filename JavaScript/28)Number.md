표준 빌트인 객체인 Number는 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공한다

래퍼 객체는 원시타입을 암묵적으로 객체의 메서드를 사용할 수 있게 감싸는 객체를 말한다

표준 빌트인 객체인 Number 객체는 생성자 함수 객체다 따라서 new 연산자와 함께 호출하면 Number 인스턴스를 생성할 수 있다

인수로 숫자가 아닌 값을 전달하면 인수를 숫자로 강제 변환한다

new연산자를 사용하지 않고 Number 생성자 함수를 호출하면 명시적 타입 변환으로 인스턴스가 아닌 숫자를 반환한다

Number 메서드인 isInteger, isNaN은 전역 함수인 isNaN과 다르게 암묵적 형변환을 하지 않는다

소감 : 원시타입 숫자를 표준 빌트인 객체 Number의 메서드와 프로퍼티로 다룰수 있게 해준다