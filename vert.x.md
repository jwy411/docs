# vert.x: 비동기 서버 프레임워크.

## 개념

### Vert.x instance

하나의 Vert.x 서버 프로세스

### Event Loop (EL)

말그대로 이벤트 목록들을 루프 돌면서, 이벤트가 발생한 경우 적절한 이벤트 헨들러에게 전달하는 역할.
EL은 Single Thread로 동작하며, 보통 한개당 20,000개 정도의 Connection을 처리.

### Event Bus
Message Queue와 같은 개념으로, Verticle 간에 통신이나, Vert.x Instance간의 통신이 가능하게 한다.


### Verticle

Vert.x에서 수행하는 하나의 프로세스.

#### Verticle Instance

Verticle 코드가 로딩되어 객체화 된것.
각각 독립된 EL 안에서 수행되고, Thread Safe 하다. (EL이 Single Thread로 동작하기 때문)

#### Worker Verticle

Message Subscriber, event bus 이용해서 받은 메시지를 처리하고 그 결괏값을 event bus를 이용해
호출자에게 보내는 방식.
예를들어 100ms 걸리는 요청을 100개의 커넥션이 요청할 경우 Worker Verticle을 이용하지 않는다면,
특정 사용자가 응답을 받기까지 10초가 걸린다 (100ms * 100) 하지만, Worker Verticle 방식을 이용한다면
시간이 걸리는 요청을 event bus를 통해 worker verticle 에게 전달 worker verticle은 처리 한뒤 다시 event bus로 전달하면 다음 EL이 돌때 
event bus로 보내진 메시지를 받고 응답 처리를 한다.
즉, 100개의 커넥션 모두 처리가 완료되길 기다리지 않아도 된다.



