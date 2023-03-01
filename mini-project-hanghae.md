## Image upload

```jsx
instance.post('/api/blogs', 
	{image},
	{headers: {"Content-Type":"multipart/form-data"}}
```

image가 formData 객체이기 때문에 전달을 할 때 객체로 감싸서 전달하게 되면 안되는 것이었다.

완성 코드

```jsx
const onChangeImgInputHandler = (e) => {
    const img = e.target.files[0];
    setImage(img);
  };
  const onSubmitHandler = async (e) => {
    e.preventDefault();
    if (!title) {
      alert("제목을 입력해주세요");
      return;
    }
    if (!contents) {
      alert("내용을 입력해주세요");
      return;
    }

    const body = {
      title,
      contents,
    }
    const formData = new FormData(); // image file을 받을 때 type (기본타입이 multipart/)
    formData.append('image', image);

    const json = JSON.stringify(body);
    const requestDto = new Blob([json], { type: 'application/json' });  // json 으로 만들어 주기 위한 것
    formData.append('requestDto', requestDto);

    instance.post('/api/blogs', 
    formData,
    {headers: {"Content-Type":"multipart/form-data"}}
    )
```

formData안에 image, requestDto이름으로 담아서 보내면 된다.
