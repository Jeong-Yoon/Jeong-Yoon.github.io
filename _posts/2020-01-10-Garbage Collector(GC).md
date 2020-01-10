# Garbage Collector(GC)
<img src="{{ site.baseurl }}/images/gc.png" style="width:600px;">

- 참조되지 않은 객체들을 탐색 후 삭제하는 역할
- 삭제된 객체의 메모리를 반환하며 Heap 메모리의 지속적인 재사용이 가능하도록 한다.
<br>
<br>

## GC 객체의 생명 주기
- Created (생성)
- In use or reachable (사용 중)
- Invisible (사용 중 but 접근 불가)
- Unreachable (사용 되지 않음)
- Collected (GC 대상이 됨)
- Finalized (Finalize 를 거친 상태)
- Deallocated (메모리 해제 된 상태)


### Created(생성)
- 먼저 객체를 위한 메모리 공간을 Heap에 할당한 다음 Super Class 의 생성자 호출을 한다.
- Initializer 및 instance variable 의 initialize를 수행 한 후 해당 객체의 생성자를 수행한다.
  * Initializer 이란 Class 코드의 Global Area에 선언된 { }사이에 기술된 코드들을 말한다. 
   * 이 Initializer들이 constructor(생성자) 보다 먼저 호출 된다.

### In use or reachable (사용 중)
- 객체가 생성되어 다른 객체에 의해 참조 되어 있는 상태이다. 이상태를 Strongly referenced 상태 라고 한다.

###  Invisible (사용 중 but 접근 불가)
- Invisible 상태는 Strongly referenced는 되어 있지만, 직접적으로 접근 할 수 없는 상태이다.
- 여기서 주의할 점은 Invisible 객체가 항상 바로 GC대상이 되지 않는 다는 것이다.


###  Unreachable (사용 되지 않음)
- strong reference가 존재 하지 않을 경우이며 Unreachable 상태의 객체는 GC의 후보가 된다.
- 여기서 후보가 된다는 것은 바로 GC가 된다는 게 아니라, GC대상 큐에만 들어간다는 개념이다.
- 이러한 객체들은 GC의 루트가 가지는 체인에 참조되는 형태이며, GC가 수행될 때 이 루트의 체인을 따라가며 메모리 해제를 한다.

###  Collected (GC 대상이 됨)
- 메모리 해제 단계의 도입부이다.
- 이 상태에서는 GC가 해당 객체의 finalize() function이 정의되어 있는지 판단을 한다.
- finalize가 있다면 finalizer라는 queue에 넣고, 없다면 바로 다음 단계인 Finalized 상태로 전환 시킨다.

###  Finalized (Finalize 를 거친 상태)
- Finalizer에 의해 finalize가 실행된 후의 상태
- finalize는 Collected 상태라고 바로 수행되는 것이 아니라, Finalizer의 Queue에 들어가는 것이기 때문에 해당 객체의 finalize가 불러지는 타이밍은 보장되지 않는다. JVM에 따라서 수행 시간도 다르다.
- GC를 수행함에 있어 객체에 finalize가 구현되어 있다면 객체의 반환시간은 그만큼 더 늦어진다. finalize를 위한 객체의 메모리도 그만큼 증가한다.
    * finalize는 한 객체에 대해 한번만 실행된다.

###  Deallocated (메모리 해제 된 상태)
- 메모리의 반환이 끝난 상태로, GC의 동작이 마무리 된다.
<br>
<br>
<br>
<br>

## Minor Garbage Collection
- New 영역에서 일어나는 Garbage Collection
- Eden 영역에 객체가 가득 차게 되면 첫 번째 Garbage Collection이 발생한다.
- Survivor1 영역에 값이 복사되고, Survivor1 영역을 제외한 나머지 영역의 객체들을 삭제한다.
- Eden 영역과 Survivor1 영역의 메모리가 기준치 이상일 경우, Eden 영역에 생성된 객체와 Survivor1 영역에 있는 객체 중 참조되고 있는 객체가 있는지 검사한다.
- 참조되고 있는 객체를 Survivor2 영역에 복사한다.
- Survivor2 영역을 제외한 영역의 객체들을 삭제하고 일정시간 이상 참조되고 있는 객체들은 Old 영역으로 이동한다.

## Major Garbage Collection
- Old영역에 있는 모든 객체들을 검사한다.
- 참조되지 않은 객체들을 한꺼번에 삭제한다.
- Minor Garbage Collection에 비해 시간이 오래 걸리고 실행 중 프로세스가 정지된다.

