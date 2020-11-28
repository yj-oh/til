# image 업로드 전 미리보기
- `new FileReader()` 사용

### 예제
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Test</title>
    <style>
        #preview {
           max-width:300px;
        }
    </style>
</head>
<body>
<div id="wrap">
    <input type="file" name="file" onchange="setPreview(event)" /><br/>
</div>

<script type="text/javascript">
    function setPreview(event) {
        const input = event.target;
        
        const img = document.createElement('img');
        img.id = 'preview';
        
        const reader = new FileReader();
        reader.readAsDataURL(input.files[0]);
        
        reader.onload = function (e) {
            img.src = e.target.result.toString();
            document.querySelector('#wrap').appendChild(img);
        };
    }
</script>
</body>
</html>
```
![](.%5B20201128%5D_preview_image_images/95836888.png)
