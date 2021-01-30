# useEffect vs useLayoutEffect

## useEffect
- 클래스 기반의 lifecycle methods 
  `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`를
  함수형 컴포넌트에서 쓰기 위한 Hooks
- 렌더링 후 실행됨
- 한 마디로 화면이 다 그려진 후에 실행됨

## useLayoutEffect
- As far as scheduling, 
  this works the same way as `componentDidMount` and `componentDidUpdate`.
- DOM 업데이트 직후, 화면이 그려지기 전 실행됨

## useEffect vs useLayoutEffect
- useLayoutEffect : DOM을 변경해야 할 때. or do need to perform measurements
- useEffect : DOM과 전혀 상관 없는 동작들. `seriously, most of the time you should use this`

##### * Reference : https://kentcdodds.com/blog/useeffect-vs-uselayouteffect
