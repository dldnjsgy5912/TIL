## Redux vs Zustand

Redux는 많은 사람들이 사용하는 좋은 상태관리 라이브러리입니다. 하지만 Redux는 초기 설정시 너무 복잡하고 장황한 코드를 입력해야합니다. 새 스토어를 정의해야 할 때마다 이러한 방식을 반복해야하는것이 가장 문제였습니다.

Redux 별칭 RTK의 툴킷은 이 문제를 줄여주었습니다. 이제 전체 저장소를 작업, 리듀서 및 상태를 포함하는 하나의 파일에 Slice로 작성할 수 있습니다. Slice 인해 RTK는 스토어 생성에 필요한 시간을 많이 줄였습니다. 그래도 아직은 너무 과하다는 생각이 듭니다.

간단한 예를 들어보겠습니다. 아래, bear의 수를 관리하는 작은 store를 만들었습니다.

**RTK **

```js
import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'bear',
  initialState: {
    value: 0,
  },
  reducers: {
    increasePopulation: (state: { value: number }) => {
      state.value += 1;
    },
    removeAllBears: (state: { value: number }) => {
      state.value = 0;
    },
  },
});

export const { increasePopulation, removeAllBears } = counterSlice.actions;

export default counterSlice.reducer;
```

**Zustand**

```js
import create from 'zustand';

const useBearStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state: { bears: number }) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}));

export default useBearStore;
```

보시다시피 Zusstand는 그것을 매우 간단하게 만듭니다. store을 짓는 방법에 대해 너무 많은 시간을 낭비할 필요가 없습니다.하나의 파일에 모든 것을 관리할수있습니다.
