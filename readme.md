# 코틀린 스터디

* 코틀린 1.2 레퍼런스 문서 번역한 것을 가지고 스터디한 내용을 정리
* http://javacan.tistory.com/entry/kotlin-11-12-ko-reference


## 기초

### kotlin의 기본 타입

* 코틀린에서 모든 것은 다 객체(스칼라랑 비슷한 듯)
* 기본 타입으로는 숫자, 문자, 불리언, 배열, 문자열
* 기본 타입의 경우 런타임 시에 기본 값으로 표현되지만 실제 유저가 사용할 때는 일반 클래스처럼 보인다(첫 글자가 대문자)

#### 숫자

* 자바랑 비슷하지만 완전하게는 같지 않음
* 코틀린의 경우 숫자에 대해 넓은 타입으로의 자동 변환을 지원하지 않는다.
```kotlin
    val a:Int = 100
    val b:Long = 200L
    
    println(a == b);   // a랑 b랑 타입이 다르기 때문에 에러 발생 코트린은 자동 변환을 지원하지 않는다.
    println(a == b.toInt()); // 이런식으로 해야함.
```

* 코틀린이 제공하는 내장 타입은 자바랑 유사
   * Double(64), Float(32), Long(64), Int(32), Short(16), Byte(8)

```kotlin
//10진수 표현
val a:Int = 100
val b:Long = 200L

val e:Double = 100.0
val f:Float = 100.0F

//16진수
val a:Int = 0xEF

//2진수
val a:Int = 0b1010111111

//8진수는 지원하지 않음

//가독성을 위해서 _를 이용할 수 있음

val a:Int = 1_000_000
```

* null 가능 숫자레퍼런스가 필료하면 Int? 이런 식으로 뒤에 ?를 추가한다. 이런식으로 표현하면 박싱 타입으로 저장
* 여기서 코틀린의 ===, == 의 차이를 알아야 할 것 같다.(자바에서는 == 과 toEqual의 차이)

   * ===(Referential Equality: 참조적 동등,identity 라고도 함) : 동일한 위치를 참조하는지 아닌지를 판단(자바에서는 ==)
   * ==(Structural Equality: 구조적 동등, equality 라고도 함): 값이 같은지 아닌지를 판단(toEqual))

   ```kotlin
   val a = Integer(10)
   val b = Integer(20)

   println(a === b)  //false
   println(a == b)  //true
   ```

* 숫자를 박싱하면 Referential Equality을 유지 하지 않는다.
```kotlin
val a: Int = 10000
val b: Int = 10000
print(a === b) // 'true'  ? 왜? 

val boxedA: Int? = a
val anotherBoxedA: Int? = a
print(boxedA === anotherBoxedA) // !!!'false' 출력!!!
```

* 하지만 Structural Equality 는 유지가 된다.
```kotlin
val a: Int = 10000
val b: Int = 10000
print(a == b) // 'true'  

val boxedA: Int? = a
val anotherBoxedA: Int? = a
print(boxedA == anotherBoxedA) // true
```

* 코틀린은 형변환을 전부 명시적으로 해야 한다.
```kotlin
val b: Byte = 1 // OK, 리터럴은 정적으로 검사함
val i: Int = b // ERROR

val i: Int = b.toInt() // OK: 명시적으로 넓힘
```
* 모든 숫자 타입은 다음 변환을 지원한다.
   * toByte(): Byte
   * toShort(): Short
   * toInt(): Int
   * toLong(): Long
   * toFloat(): Float
   * toDouble(): Double
   * toChar(): Char

* 숫자에 대한 표준 수치 연산을 지원, 이들 연산에 알맞은 클래스의 맴버로 선언되어 있다.
* 비트 연산자
   * shl(bits) 부호있는 왼쪽 시프트 (자바의 << )
   * shr(bits) 부호있는 오른쪽 시프트 (자바의 >> )
   * ushr(bits) 부호없는 오른쪽 시프트 (자바의 >>> )
   * and(bits) 비트 AND
   * or(bits) 비트 OR
   * xor(bits) 비트 XOR
   * inv() 비트 역
* 수치 연산
   * ==, != 동등함 비교
   * <, >, <=, => 비교 연산자
   * a..b : 범위 생성, x in a..b (x가 a 값과 b 값 사이에 있나?), x !in a..b (x가 a 값과 b 값 사이에 없나?)
