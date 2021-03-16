# CSS Animation
Property | Description
--- | ---
animation-name | @keyframes 속성에 지정한 애니메이션 이름
animation-duration | 재생 시간 (단위 : ms, s)
animation-delay | 시작 지연 시간 (단위 : ms, s)
[animation-direction](#animation-direction) | 애니메이션 종료 후 액션 : 처음부터 시작, 역방향으로 재생, 번갈아 재생
animation-iteration-count | 애니메이션 실행 횟수
animation-play-state | `running` or `paused`
[animation-timing-function](#animation-timing-function) | 애니메이션 속도 곡선 지정
[animation-fill-mode](#animation-fill-mode) | 애니메이션이 재생되지 않을 때의 스타일 지정


## animation-direction
- 애니메이션 종료 후 액션 : 처음부터 시작, 역방향으로 재생, 번갈아 재생

Value | Description
--- | ---
normal | 정방향 `default`
reverse | 역방향
alternate | 정방향으로 시작해서 역방향 번갈아가며 반복
alternate-reverse | 역방향으로 시작해서 정방향 번갈아가며 반복


## animation-timing-function
- 애니메이션 속도 곡선 지정

Value | Description
--- | ---
ease | 천천히 시작, 빠르게, 천천히 종료 `default`
linear | 일정한 속도
ease-in | 천천히 시작
ease-out | 천천히 종료
ease-in-out | 천천히 시작, 천천히 종료
cubic-bezier(n,n,n,n) | 사용자가 지정한 cubic-bezier function에 따라

## animation-fill-mode
- 애니메이션이 재생되지 않을 때의 스타일 지정

Value | Description
--- | ---
none | 스타일 적용하지 않음 `default`
forwards | 마지막 keyframe에서 설정한 스타일 값 유지 (depends on animation-direction and animation-iteration-count)
backwards | 처음 keyframe (depends on animation-direction) 에서 설정한 스타일 값 적용, animation-delay 동안 유지
both | forwards, backwards 양쪽 규칙을 따르고 양방향으로 확장


## +) 
- 한 줄로 작성할 수도 있음
```
animation: name, duration, timing-function, delay, iteration-count, direction, 
           fill-mode, play-state;
```
ex)
```css
#example {
    /* name | duration | timing-function | iteration-count | direction */
    animation: move 2s linear 2 reverse;
    /* keyframe move를 2초 동안 일정한 속도로 2회 역방향 재생 */
}
```

##### * References
- https://www.w3schools.com/css/css3_animations.asp
- https://developer.mozilla.org/en-US/docs/Web/CSS/animation

##### * 함께보기
- [@keyframes]([20210316]_keyframes.md)
