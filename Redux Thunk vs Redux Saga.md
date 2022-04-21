> Redux Thunk 와 Redux Saga 둘다 비동기함수를 처리할수 있게 해주는 도구이다.

### Redux Thunk

**장점**

- 사용 방법이 간단하다.

**단점**

- 초보가 작업을 하게 되면 Action creator에서 콜백 hell에 빠질 수 있다
  unit test시에 불편함이 있다. 연결이 다 되어 있다보니, 잘라서 테스트가 쉽지 않다.
  saga에서 제공해주는 것들이 없다 (단점이 아닐 수도 있지만, saga의 편의성이 있기때문에 적어보았습니다

### Redux Saga

**장점**

- Action이 매우 깔끔하게 디자인할 수 있습니다. (정말 크죠) && 테스트에 매우 용이 합니다.

**단점**

- 처음에 셋업할게 좀 있으며, generator등의 새로운 개념도 숙지 하셔야 합니다. (공부할게 추가!) → 하지만, 한 번 셋업을 해두면, 어렵지 않습니다.

### 리덕스 미들웨어란?

액션과 리듀서에 들어가는 그순간까지 실행시켜주는 함수

### Thunk

```
const thunkExample = () => {
	return async function (dispatch) => {
		const items = await fetch("https://www.~~~~~")
		if (items) {
			dispatch({
				type: "ADD",
				payload: items.json()
			})
		}
	}
}
```

thunk가 async하게 API콜도 하고, 그 후에, 최종적으로는 synchronous 한 action을 dispatch해주게 합니다.

```
{type: "ADD_STATE", payload: items.json()} //-> 요것이 액션!
```

### Saga

Saga 는 Thunk 와 마찬가지로 비동기적으로 함수를 처리할수있지만 generators 를 사용하는 차이가 있습니다.
generators의 가장큰 장점은, 중간에 엑스큐션을 멈췄다가, 끝낼 수도 있고, 다시 시작할 수 도 있습니다. 실전에서 이게 왜 필요할까요? (실전에서 이 일들이 발생하는 사례 케이스는 다음에 한 번 만들어 보겠습니다)

```
function* someGeneratorFunction() {
	yield('good')
	yield('better')
}

let itr = someGeneratorFunction();
console.log(itr.next()) // {value: "good", done: false}
console.log(itr.next()) // {value: "better", done: false}
console.log(itr.next()) // {value: undefined, done: true}

```

저희가 saga를 generator를 직접 콜을 해서 .next()를 실행할 일은 없습니다. generator를 설명하고나 직접 실행했을때를 보여주는 용도로 작성된 코드 입니다

```
import {call, put, takeEvery, all,} from 'redux-saga/effect';
import Api from '...' //<-- 여기는 각자마다 경로가 다르겠죠!

function* fetchUser(action) {
	try{
    const userData = yield call(Api.fetchUser, action.payload.userId);

		yield put({type: 'USER_FETCH_SUCCEEDED', payload: userData.json()});
	} catch (e) {
		yield put({type: "USER_FETCH_FAILED", message: e.message.});
	}
}

function* mySaga() {
	yield takeEvery("USER_FETCH_REQUESTED", fetchUser);
}

export default function* rootSaga() {
	yield all([
		mySaga(),
		//다른 사가도 여기에 추가 하기!
	])
}
```
