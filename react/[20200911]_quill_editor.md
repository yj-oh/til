# Quill editor

```
yarn add quill
```
```javascript
import Quill from 'quill';
import 'quill/dist/quill.snow.css';
```

```javascript
const QuillWrapper = styled.div``;

const Editor = () => {
  const quillElement = useRef(null);
  const quillInstance = useRef(null);

  useEffect(() => {
    quillInstance.current = new Quill(quillElement.current, {
      theme: 'snow',  // bubble or snow
      placeholder: '내용을 작성하세요',
      modules: {
        toolbar: [
          [{ 'header': [1, 2, 3, 4, 5, 6, true] }],
          [{ 'size': ['small', false, 'large', 'huge'] }],
          ['bold', 'italic', 'underline', 'strike'],
          [{ 'color': [] }, { 'background': [] }],
          [{ list: 'ordered' }, { list: 'bullet' }],
          ['link', 'image'],
        ],
      },
    });
  }, []);

  return (
    <QuillWrapper>
      <div ref={quillElement} />
    </QuillWrapper>
  );
};

export default Editor;
```

#### toolbar options
- https://quilljs.com/docs/modules/toolbar
