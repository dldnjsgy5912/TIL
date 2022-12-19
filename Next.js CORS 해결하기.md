CORS는 Cross-Origin Resource Sharing의 약자입니다. 교차 출처 리소스 공유로 번역될 수 있는데,** 브라우저에서 다른 출처의 리소스를 공유**하는 방법입니다.

출처(Origin) 는 Protocol, Host, Port 를 모두 합친 것을 의미합니다.

ex) https://www.github.com:443

> Next.js CORS 해결하기

```js
//next.config.js
 async rewrites() {
   return [
     {
       source: '/api/:path*',
       destination: `http://주소/:path*`,
     },
   ];
 },
```

next.config.js 에서 위와같이 설정을 해준다.

```js
const url2 = `/api/나머지 주소`;
```

호출시 이런식으로 /api/ 뒤에 원하는 호출 주소를 적어주면 된다.
