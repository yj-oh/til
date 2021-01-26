# Line 그래프 그리기 - using react-chartjs-2

## package 설치
```
npm install chart.js
npm install react-chartjs-2

or

yarn add chart.js
yarn add react-chartjs-2
```

## 예제
```jsx
import React from 'react';
import { Line } from 'react-chartjs-2';

const data = {
    labels: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
    datasets: [
        {
            label: 'number data',
            data: [10, 1000, 300, 2, null, 200, 800],
            fill: false,      // 라인 내부 영역 색 채움
            spanGaps: true,   // 데이터 null일 때 선 이어짐
            tension: 0,       // Line 곡선
            borderWidth: 5,   // Line 굵기
            borderColor: 'rgba(255, 99, 132, 0.2)',
            backgroundColor: 'rgb(255,175,20)',
        },
    ],
};
const graphOptions = {
    tooltips: {
        titleFontSize: 18,
        titleAlign: 'center',
        bodyFontSize: 18,
        bodyAlign: 'center',
        displayColors: false,
    },
};

const Graph = () => {
    return (
        <div style={{ width: '800px' }}>
            <h2 className='title'>Graph Test</h2>
            <Line data={data} options={graphOptions} />
        </div>
    );
};

export default Graph;

```

## 결과
![graph](.%5B20210127%5D_react-chartjs-2_images/12bbf57a.png)

- Github : https://github.com/reactchartjs/react-chartjs-2
- demo page : http://reactchartjs.github.io/react-chartjs-2/#/
- Chart.js : https://www.chartjs.org/
