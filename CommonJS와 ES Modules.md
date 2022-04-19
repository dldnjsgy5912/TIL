> CJS의 경우 require()와 module.exports를 사용하며, ESM은 import와 export를 사용한다.

1. ESM에서는 require()를 사용할 수는 없다. 오로지 import만 가능하다.
2. CJS도 마찬가지로 import를 사용할 수는 없다.
3. ESM에서 CJS를 import하여 사용할 수 있다. 그러나 오로지 default import만 가능하다. import \_ from 'lodash' 그러나 CJS가 named export를 사용하고 있다면 named import import { shuffle } from 'lodash와 같은 것은 불가능하다.
4. ESM을 CJS에서 require()로 가져올 수는 있다. 그러나 이는 별로 권장되지 않는다. 그 이유는 이를 사용하기 위해서는 더 많은 boilerplate가 필요하고, 최악의 경우 Webpack이나 Rollup 같은 번들러도 필요 하다. 그 이유는, ESM가 require()에서 어떻게 동작해야 하는지 모르기 때문이다.
5. CJS는 기본값으로 지정되어 있다. 따라서 ESM 모드를 사용하기 위해서는 opt-in해야 한다. .js를 .mjs로 바꾸거나, package.json에 "type": "module" 옵션을 넣는 방법이 있다. (기존에 CJS를 쓰던 것은 .cjs로 바꾸면 된다.)

**cjs개념**

개념은 간단하다. '.js' 파일 간의 어떻게 의존성을 가지게 할지 정해주는 것이다.
우선 commonJS라는 개념이 존재하는 이유는, 자바스크립트를 범용적으로 모듈화를 높이기 위함!

### export

```
// test1.js

function MSG1(){
  console.log('1');
}
function MSG2(){
  console.log('2');
}

export {MSG1, MSG2}
```

위 코드를 보면, test1.js에서 MSG1, MSG2의 함수를 export 한다. export는 다른 곳에서 쓸 수 있게 내보내 주는 것.

export 키워드 뒤에는 내 보낼 함수 혹은 변수명을 {}괄호로 묶어줘서 보낸다. 이름을 꼭 맞춰주어야 한다.

```
// test2.js

import {MSG1, MSG2} from './test1'

MSG1(); // '1'
```

test2.js 파일에서 test1.js에서 내보냈던 함수 두개를 가져오는데, import 키워드를 쓰고 뒤에 해당 함수명을 가져온다.(중괄호 사용은 jsx문법) 뒤에 from 키워드를 쓰고 해당 함수의 파일 경로를 적어준다.

그러면 위와 같이 함수를 사용할 수 있다.

파일 경로와 함수 및 변수명이 맞아야 한다. 단, export시에 딱 하나만 넘겨줄 경우 빼고!

### export default

```
// test1.js

function MSG1(){
  console.log('1');
}

export default MSG1
```

```
// test2.js

import MSG3 from './test1'

MSG3(); // '1'

```
