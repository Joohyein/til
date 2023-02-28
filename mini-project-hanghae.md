이미지, 제목, 내용을 보내는데 이미지가 백엔드에서 안받아와지는데 추측으로는 프로트엔드와 백엔드가 주고 받는 타입이 달라서 오류가 나는 것 같다. 

## error

```jsx
POST http://3.36.51.159:8080/api/blogs 400
```

```jsx
settle.js:19 Uncaught (in promise) 
AxiosError {message: 'Request failed with status code 400', name: 'AxiosError', code: 'ERR_BAD_REQUEST', config: {…}, request: XMLHttpRequest, …}
code
: 
"ERR_BAD_REQUEST"
config
: 
{transitional: {…}, adapter: Array(2), transformRequest: Array(1), transformResponse: Array(1), timeout: 0, …}
message
: 
"Request failed with status code 400"
name
: 
"AxiosError"
request
: 
XMLHttpRequest {onreadystatechange: null, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}
response
: 
{data: {…}, status: 400, statusText: '', headers: AxiosHeaders, config: {…}, …}
stack
: 
"AxiosError: Request failed with status code 400\n    at settle (http://localhost:3000/static/js/bundle.js:57049:12)\n    at XMLHttpRequest.onloadend (http://localhost:3000/static/js/bundle.js:55744:66)"
[[Prototype]]
: 
Error
```

![이미지 2023. 3. 1. 오전 1.02.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79208cc0-be72-4bff-9730-fdcb0971ea57/%E1%84%8B%E1%85%B5%E1%84%86%E1%85%B5%E1%84%8C%E1%85%B5_2023._3._1._%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.02.jpeg)

**react code**

```jsx
const onChangeImgInputHandler = (e) => {
    const img = e.target.files[0];
    // console.log('img :', img);
    const formData = new FormData();
    formData.append('image', img);
    // console.log(formData);
    // for (const keyValue of formData) console.log(keyValue);
    setImage(formData);
    // console.log(formData.get('image'));
  }

  const onSubmitHandler = async (e) => {
    e.preventDefault();
    if(!title) {
      alert("제목을 입력해주세요");
      return;
    }
    if(!contents) {
      alert("내용을 입력해주세요");
      return;
    }
    // const image = imagea;
    const body = {
      title,
      contents,
    }
    // console.log("body: ", body);
    const json = JSON.stringify(body);
    // console.log("json", json);
    const requestDto = new Blob([json], { type: 'application/json' });
    // console.log("blob", blob);
    // image.append('requestDto', blob);
    console.log("image", ...image);
    // formDataImg.append("title", JSON.stringify(title));
    // formDataImg.append("contents", JSON.stringify(contents));
    console.log("formDataImg: ", image.get("image"));
    // console.log("formDataImg: ", image.get("requestDto"));
    instance.post('/api/blogs', 
    {image, requestDto},
    {headers: {"Content-Type":"multipart/form-data"}}
    )

  };
```
