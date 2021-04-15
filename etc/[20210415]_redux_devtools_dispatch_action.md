# Redux devtools로 dispatch action 실행하기
- 브라우저에서 어떠한 현상을 임의로 재현해야 할 상황이 있었음.
- 관련해서 찾아보다가 브라우저에서 action을 실행할 수 있는 방법이 있다는 걸 알게 됨.
- `Redux devtools`를 사용한다.

![](.%5B20210415%5D_redux_devtools_dispatch_action_images/3b6dedec.png)

```text
{
type: 'IMPORT_STATE',
... whatever payload contents you need here ...
}
```
- https://stackoverflow.com/questions/57769943/how-to-dispatch-an-action-to-the-redux-devtools-store-for-importing-a-state-from
