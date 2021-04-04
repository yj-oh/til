# Asset Modules
- 추가 loader(raw-loader, url-loader, file-loader)를 구성하지 않아도 
  fonts, icons, images 등의 asset files 사용 가능
- `asset/resource` emits a separate file and exports the URL (file-loader)
- `asset/inline` exports a data URI of the asset (url-loader)
- `asset/source` exports the source code of the asset (raw-loader)
- `asset` automatically chooses between exporting a data URI and emitting a separate file.

## Resource assets
- 이미지 번들링, 경로 설정

### webpack.config.js
```javascript
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'main.js',
        path: path.resolve(__dirname, 'dist'),
    },
    module: {
        rules: [
            {
                test: /\.png/,
                type: 'asset/resource'
            }
        ],
    },
};
```
- 모든 png 파일이 output으로 내보내지고 path가 번들에 삽입된다.

### src/index.js
```javascript
import myImage from './images/myImage.png';

img.src = myImage;
```

* Reference : https://webpack.js.org/guides/asset-modules/
