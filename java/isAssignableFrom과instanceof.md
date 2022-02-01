# Class.isAssignableFrom vs instanceof

> 출처 : https://stackoverflow.com/questions/496928/what-is-the-difference-between-instanceof-and-class-isassignablefrom

## instanceof

- 부모 instanceof 자식클래스 : false
- 자식 instanceof 부모클래스 : true
- 자식(부모클래스로 형변환됨) instanceof 자식클래스: true

## Class.isAssignableFrom

- 부모.Class.isAssignableFrom(자식.getClass()) : true
- 자식.Class.isAssignableFrom(부모.getClass()) : false
- 자식.Class.isAssignableFrom(자식(부모클래스로 형변환됨).getClass()) : true

## 차이점

- instanceof는 컴파일 시점에서 클래스를 알고 있어야 한다.
- isAssignableFrom()은 런타임 중에 동적으로 변할 수 있는 상황에서 사용할 수 있다.
- 성능은 instanceof가 더 좋다.
