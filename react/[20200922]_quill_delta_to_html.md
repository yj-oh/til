# quill-delta-to-html

### Package install
```
yarn add quill-delta-to-html
```

### Data format : delta
```json
{
  "ops": [
    {
      "insert": "Hello, world!\n"
    },
    {
      "insert": {
        "image": "https://google.com"
      }
    },
    {
      "insert": "\n"
    }
  ]
}
```
### Code
- `content` : DB에서 꺼내온 String data (↑ 위의 데이터 형태)
```ecmascript 6
import { QuillDeltaToHtmlConverter } from 'quill-delta-to-html';

// delta to html
const config = {
  multiLineParagraph: false,
  renderAsBlock:true,
};
const ops = JSON.parse(content.toString()).ops;
const converter = new QuillDeltaToHtmlConverter(ops, config);
const html = converter.convert();
```
- configuration
   - 참고 : https://github.com/nozer/quill-delta-to-html
