# Java GC (Garbage Collector) 동작 원리 정리

## 1. GC란?

Java는 개발자가 직접 메모리를 해제하지 않아도 JVM이 자동으로 사용하지 않는 객체를 제거해주는 기능을 제공한다.

👉 이를 **Garbage Collector(GC)**라고 한다.

---

## 2. Heap 메모리 구조

Java의 Heap 영역은 크게 2가지로 나뉜다.

```
Heap
 ├── Young Generation
 │     ├── Eden
 │     ├── Survivor 0
 │     └── Survivor 1
 │
 └── Old Generation
```

---

## 3. 객체 생성 흐름

1. 객체는 처음 생성될 때 **Eden 영역**에 생성됨
2. Eden이 꽉 차면 GC 발생 (Minor GC)
3. 살아남은 객체는 Survivor 영역으로 이동
4. Survivor 영역에서 일정 횟수 살아남으면 Old 영역으로 이동

---

## 4. GC 종류

### 4.1 Minor GC (Young GC)

* 대상: Young Generation
* 속도: 빠름
* 특징:

  * Eden이 가득 차면 발생
  * 살아있는 객체만 Survivor로 이동

---

### 4.2 Major GC (Old GC)

* 대상: Old Generation
* 속도: 느림 (중요🔥)
* 특징:

  * Old 영역이 가득 차면 발생
  * 애플리케이션이 멈출 수 있음 (Stop-The-World)

---

## 5. GC 핵심 동작 방식

### 5.1 Mark (마킹)

* GC Root에서 시작해서 사용 중인 객체를 표시

### 5.2 Sweep (삭제)

* 사용되지 않는 객체 제거

### 5.3 Compact (압축)

* 메모리 단편화 제거
* 객체를 한쪽으로 몰아서 공간 확보

---

## 6. GC Root란?

GC가 살아있는 객체를 판단하는 기준

예시:

* 스택에 있는 변수
* static 변수
* JNI 참조 객체

👉 GC Root에서 도달 가능한 객체 = 살아있는 객체

---

## 7. Stop-The-World

GC가 실행되는 동안 모든 애플리케이션 스레드가 멈춤

👉 성능 저하의 주요 원인
👉 Major GC에서 특히 크게 발생

---

## 8. GC의 장점

* 메모리 관리 자동화
* 메모리 누수 감소
* 개발 생산성 향상

---

## 9. GC의 단점

* GC 실행 시 성능 저하
* Stop-The-World 발생
* 튜닝 필요

---

## 🔥 핵심 요약

* Eden → Survivor → Old 이동 구조
* Minor GC는 빠름 / Major GC는 느림
* Mark → Sweep → Compact
* Stop-The-World 발생 가능
