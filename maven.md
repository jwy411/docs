
### Optional Dependencies
![image](https://user-images.githubusercontent.com/3205565/69951235-3d5bce00-1538-11ea-9a91-b98854974b6c.png)

가끔 mavenrepository 사이트에서 특정 Dependencies 가 _optional_ 로 표시되는 경우가 있다.

https://mvnrepository.com/artifact/io.vertx/vertx-core/3.4.2

`내 프로젝트` → `vertx-core` → `vertx-codegen` 이렇게 의존성 관계를 가지고 있을 때

일반적으로는 *의존성 전의*로 인해 `내 프로젝트` 도 `vertx-codegen` 라이브러리를 의존하게 되는데

`vertx-core` 에서 `vertx-codgen` 라이브러리를 optional 의존성으로 가지게 된다면

`내 프로젝트` 에서는 `vertx-codegen`을 의존하지 않게 된다.

https://maven.apache.org/guides/introduction/introduction-to-optional-and-excludes-dependencies.html

> Optional dependencies are used when it's not possible (for whatever reason) to split a project into sub-modules.
>
>(Optional dependencies 는 어떠한 이유에서 프로젝트를 sub module로 분리 할 수 없을 때 사용된다.)

라고 하는데 무슨 말인지 잘 모르겠다.

아무튼 `vertx-core`의 pom.xml 을 보면 빌드 시 `vertx-codegen`을 이용하여 코드를 생성하고 그 이후에는 사용되지 않기 때문에

굳이 `내 프로젝트` 에서 `vertx-codegen`을 사용할 이유가 없기 때문에 optional 옵션을 건 것이 아닐까 생각된다.

이걸 찾아보게 된 이유는 vertx-core 코드를 살펴보던중 vertx-codegen 을 통해 만들어진 일부 코드들에 대해서

IDE는 알 수 없다고 빨간색으로 표기되어 그 원인을 찾던 중 여기까지 온 것 같다.