# JSX select 특정값 선택
- 게시글 수정 에디터 화면.
- category를 selectbox로 보여주고 content의 category_id에 따라 해당 category를 선택된 채로 띄우고 싶다.
```jsx
<select
  name="category_id"
  value={content.category_id}
>
  {categories && categories.map(category => (
    <option
      key={category.id}
      value={category.id}
    >
      {category.name}
    </option>
  ))}
</select>
```
- option tag의 value값과 content의 category_id 값을 비교해서 같을 경우 
option tag에 selected 옵션을 줘야 하나 했는데 그냥 select tag의 value에 
content의 category_id 값을 넣어주면 된다.
 