# Android app - Firebase 연결

## 👉 Firebase 프로젝트 생성
- [Firebase console](https://console.firebase.google.com/u/0/) - 프로젝트 만들기
![시작하기](.%5B20201228%5D_push_01_firebase_images/85549ef5.png)
  
## 👉 react-native 프로젝트 생성
```
expo init react-native-alarm-app
```

## 👉 package 설치
```
cd react-native-alarm-app
yarn add @react-native-firebase/app
yarn add @react-native-firebase/messaging
```

## 👉 Android app - Firebase 연결
- firebase console에서 아까 생성했던 firebase project 클릭
![](.%5B20201228%5D_push_01_firebase_images/da01fdc9.png)
- 앱에 firebase 추가하여 시작하기 - Android 아이콘 클릭
![](.%5B20201228%5D_push_01_firebase_images/2bc190b6.png)
- `/android/app/src/main/AndroidManifest.xml` 파일 내부
첫 번째 `<manifest>` 태그의 `package` 속성값을 입력 (com. 으로 시작하는)
![](.%5B20201228%5D_push_01_firebase_images/316b82a4.png)
- 나머지 항목은 선택사항이다.

### ❗️ 근데 android 폴더가 없다
```
expo eject    
```
- 위의 명령어 실행하면 `android` 폴더가 생기고 내부에서 네이티브 코드에 접근할 수 있다.
- `google-services.json 다운로드` 버튼 클릭
![](.%5B20201228%5D_push_01_firebase_images/3fd4ccec.png)
- 다운로드된 파일을 `/android/app` 경로에 추가
- 페이지 설명에 나온 대로 진행하면 된다.
![](.%5B20201228%5D_push_01_firebase_images/519378a4.png)
- `/android/build.gradle`
    ```groovy
    buildscript {
      repositories {
        // 아래 코드가 있는지 확인하고, 없으면 추가
        google()  // Google's Maven repository
      }
      dependencies {
        ...
        // 아래 코드 추가
        classpath 'com.google.gms:google-services:4.3.4'
      }
    }
    
    allprojects {
      ...
      repositories {
        // 아래 코드가 있는지 확인하고, 없으면 추가
        google()  // Google's Maven repository
        ...
      }
    }
    ```
- `/android/app/build.gradle`
    ```groovy
    apply plugin: 'com.android.application'
    // 아래 코드 추가
    apply plugin: 'com.google.gms.google-services'
    
    dependencies {
        // 아래 두 줄 추가
        implementation platform('com.google.firebase:firebase-bom:26.2.0')
        implementation 'com.google.firebase:firebase-messaging:20.2.3'
    }
    ```
![](.%5B20201228%5D_android_app_and_firebase_images/f532b880.png)
- 프로젝트 rebuild
```
npx react-native run-android
```

## (+) ⚠️ BUILD FAILED
- Compatible side by side NDK version was not found.
![](.%5B20201228%5D_android_app_and_firebase_images/2b52ab2f.png)
- Android studio - SDK Manager
![](.%5B20201228%5D_android_app_and_firebase_images/926f19a9.png)
- SDK Tools - `NDK (Side by side)` 체크 - OK
![](.%5B20201228%5D_android_app_and_firebase_images/5a538653.png)
