# C# Language 

- [C#의 주요 특징 및 개념](./cs-concepts.md)
- [프로그램 구조](./program-structure.md)
- [코딩 스타일](coding-style.md)

## 타입 시스템 (Type System)

- [타입 시스템 개요](./type-system/README.md)
- [클래스](./type-system/class.md): 객체를 만들기 위한 설계도
- [인터페이스](./type-system/interface.md): 특정 기능을 구현해야 하는 명세(明細)
- [레코드](./type-system/record.md): 불변(immutable) 데이터 모델을 위한 참조 타입
- [구조체](./type-system/struct.md): 데이터 저장을 위한 값 타입 구조 (설계도)
- [열거형](./type-system/enum.md): 여러 개의 상수를 하나의 그룹으로 묶는 자료형
- [배열](./type-system/array.md)
- [제네릭](./type-system/generic.md): 특정한 데이터 타입에 의존하지 않고 일반화된(generalized) 코드를 작성할 수 있도록 하는 기능
- [튜플](./type-system/tuple.md): 여러 개의 값을 묶어서 하나의 단위로 표현하는 자료 구조
- [익명 형식](./type-system/anonymous-type.md)
- [델리게이트](./type-system/delegate.md): 메서드를 가르키는 타입 (메서드 호출을 대신 수행하는 역할)
- [이벤트](./type-system/event.md)
- [동적 타입](./type-system/dynamic-type.md)
- 추가로 알아야 할것
  - [박싱 및 언박싱](./type-system/boxing-unboxing.md): 값타입과 참조타입의 상호 변환
  - [타입 변환](./type-system/type-conversion.md)

## 객체 지향 프로그래밍 (Object Oriented Programming)

- [객체 지향 프로그래밍 개요](./oop/README.md)
- [`object` 클래스](./oop/object.md)
- [상속](./oop/inheritance.md)
- [다형성](./oop/polymorphism.md)

## LINQ

- [LINQ 개요](./LINQ/README.md)
- [쿼리 연산자](./LINQ/query-operators.md)
- [`join` 연산자](./LINQ/join-operator.md)
- [`group` 연산자](./LINQ/group-operator.md)
- [LINQ와 파일 디렉토리](./linq/LINQ-file-directory.md)

## Reflection and Attributes

- [리플렉션 및 특성 개요](./reflection-attribute/README.md)
- [사용자 지정 특성 만드는 방법](./reflection-attribute/create-custom-attributes.md)
- [제네릭과 특성](./reflection-attribute/generics-and-attributes.md)
- [리플렉션 좀 더 들여다 보기](./reflection-attribute/reflection.md)

## Asynchronous vs Parallel Programming

- [비동기 및 병렬 프로그래밍 개요](./async-vs-parallel/README.md)
- [비동기 프로그래밍](./async-vs-parallel/async-programming.md)
  - [비동기 작동 순서 다이어그램](./async-vs-parallel/async-operation-sequence-diagram.md)
  - [비동기 프로그램 예제들](./async-vs-parallel/async-examples.md)
- [병렬 프로그래밍](./async-vs-parallel/parallel-programming.md)
  - [병렬 프로그래밍 예제들](./async-vs-parallel/parallel-examples.md)
