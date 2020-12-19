# iOS notch 옆 공간(?) 커스터마이징
- 아래와 같이 노치 주변에 하얀색 공간이 있는데, 그 부분에 배경색을 본문과 동일하게 넣고 싶다.

![](.%5B20201220%5D_ios_safeareaview_images/754d3252.png)
```jsx
import React from 'react';
import NewsList from './components/NewsList';
import Categories from './components/Categories';

const App = () => {
    return (
        <>
            <Categories />
            <NewsList />
        </>
    );
};

export default App;
```

## 💡 `<SafeAreaView>`
- 현재 iOS 11 이상에만 적용됨
- https://reactnative.dev/docs/safeareaview
```jsx
import { SafeAreaView, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
    container: {
        backgroundColor: '#eaeaea',
    },
});

const App = () => {
    return (
        <>
            <SafeAreaView style={styles.container}>
                <Categories />
            </SafeAreaView>
            <NewsList />
        </>
    );
};
```
- `<Categories>` 컴포넌트를 `<SafeAreaView>`로 감싸고 style을 줬다.
- 노치 주변에 배경색상은 잘 반영되었는데 
  다크모드에서 시간, 배터리 등의 글자색이 흰색으로 바뀌어서 잘 보이지 않음.

## 💡 `<StatusBar>`
- https://reactnative.dev/docs/statusbar
```jsx
import { SafeAreaView, StatusBar, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
    container: {
        backgroundColor: '#eaeaea',
    },
});

const App = () => {
    return (
        <>
            <SafeAreaView style={styles.container}>
                <StatusBar barStyle='dark-content' />
                <Categories />
            </SafeAreaView>
            <NewsList />
        </>
    );
};
```
- `<StatusBar barStyle='dark-content' />`를 추가했다.

![](.%5B20201220%5D_ios_safeareaview_images/9bb5e63a.png)

- 노치 없는 디바이스는 이렇게 보인다.

![](.%5B20201220%5D_ios_safeareaview_images/7a901ad7.png)

## 전체 코드
- https://github.com/yj-oh/react-native-news-app
```jsx
import React from 'react';
import { SafeAreaView, StatusBar, StyleSheet } from 'react-native';
import NewsList from './components/NewsList';
import Categories from './components/Categories';

const styles = StyleSheet.create({
    container: {
        backgroundColor: '#eaeaea',
    },
});

const App = () => {
    return (
        <>
            <SafeAreaView style={styles.container}>
                <StatusBar barStyle='dark-content' />
                <Categories />
            </SafeAreaView>
            <NewsList />
        </>
    );
};

export default App;
```
