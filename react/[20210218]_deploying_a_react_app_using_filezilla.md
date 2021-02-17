# Deploying a react app using FileZilla

## 1. Download FileZilla
- https://filezilla-project.org/

## 2. Click the button
![FileZilla](.%5B20210218%5D_deploying_a_react_app_using_filezilla_images/e0179591.png)

## 3. Configure
![](.%5B20210218%5D_deploying_a_react_app_using_filezilla_images/7f99b97a.png)

## 4. build 

### package.json
```json
{
  // ...
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```
```
npm run build
// or
yarn build
```
- This is creates a `build` directory in the root directory.
- In your app directory of your FileZilla FTP, you can copy the `build` folder.
