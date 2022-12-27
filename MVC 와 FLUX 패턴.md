# MVC 패턴

![](https://velog.velcdn.com/images/dldnjsgy5912/post/bb055d2d-71a0-408a-9907-0a79d45f7473/image.png)

MVC는 Model, View, Controller의 약자입니다. Model에 데이터를 저장하고, Controller를 이용하여 Model의 데이터를 관리(CRUD)합니다. Model의 데이터가 변경되면 View로 전달되어 사용자에게 보여집니다. 또한 사용자가 View를 통해 데이터를 입력하면 View 역시 Model을 업데이트할 수 있다는 점입니다. **즉 데이터가 양방향으로 흐를 수 있다는 것이죠.**

# MVC 문제점

![](https://velog.velcdn.com/images/dldnjsgy5912/post/13ab4a57-23ef-4fd2-9ee6-43a3b2d3b157/image.png)
View가 다양한 상호작용을 위해 여러 개의 Model을 동시에 업데이트하고 Model 역시 여러 개의 View에 데이터를 전달하는 상황이 발생합니다.
이렇게 많은 의존성을 가지면 Model의 개수가 많아질수록 각 Model에서 발생한 이벤트가 애플리케이션 전체로 퍼져나갈 때 이를 예측하기 힘들어 집니다.

페이스북은 “MVC는 정말 눈 깜짝할 사이에 복잡해진다”고 말하며 이 문제의 해결 방안으로 단방향 데이터 흐름을 가지는 Flux 패턴을 고안해냈습니다.

# Flux 패턴

![](https://velog.velcdn.com/images/dldnjsgy5912/post/1295465f-df96-4720-a585-3ea21b32315a/image.png)

Flux는 사용자 입력을 기반으로 Action을 만들고 Action을 Dispatcher에 전달하여 Store(Model)의 데이터를 변경한 뒤 View에 반영하는 단방향의 흐름으로 애플리케이션을 만드는 아키텍처입니다.
![](https://velog.velcdn.com/images/dldnjsgy5912/post/dbbb38b0-2659-4e78-9497-d14bfb56e391/image.png)

![](https://velog.velcdn.com/images/dldnjsgy5912/post/4cc5d7bf-76c2-435c-b758-2e0cd6bf1bba/image.gif)

위와 같이 상태관리 라이브러리는 보통 Flux 패턴을 지니고 있습니다.(REDUX, ZUSTAND)

각 요소들은 단방향 흐름에 따라 순서대로 역할을 수행하고, View로부터 새로운 데이터 변경이 생기면 처음부터 다시 이 순서대로 실행합니다. 이렇게 함으로써 예외 없이 데이터를 처리할 수 있게 되었습니다.
