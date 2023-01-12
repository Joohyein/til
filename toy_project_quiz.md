# 4일차

### 오늘 할 일
index페이지에서 문제를 제출했을 때 화면에 보여지는 이미지목록을 최근에 제출한 이미지가 위로 오도록 순서를 뒤집어 주는 작업을 했다. index.js에서 작성한 for문을 수정해줬다. 

```javascript
for (let i = rows.length - 1; i >= 0; i--) {
    const image = rows[i]['quiz_ans']
    const key = rows[i]['quiz_key']

    $('.quizList > ul').append(`<a id="${key}" href = "/quizSolve?quizKey=${key}"><li>
                                    <img src="/static/image/${image}.png">
                                    </li></a>`);
}
	
```

### 문제
rows.length가 0일 때 for문을 돌아서 오류가 났다

### 해결
if문을 추가해서 rows.length가 0이면 return해주도록 했다.
```javascript
if(rows.length === 0) {
	return
}
```

- 알게된 점
    
    for문을 작성할 때는 범위를 잘 체크해야겠다는 것을 다시 깨달았다.
    
    아직 자바스크립트가 익숙하지 않아서 처음에 ‘==’으로 작성했는데 ‘==’는 비교하는 두 값의 데이터타입이 일치하지 않을 때 해당 값의 데이터타입을 자동으로 변환해주는 특징이 있어서 ‘===’으로 바꿔줬다.
    
     === 는 엄밀한 (strict) 일치연산자여서 비교하는 두 값의 데이터타입과 값 자체가 정확히 일치해야만 true를 리턴한다. 정확한 프로그래밍을 위해 ===을 쓰는 것을 습관화 해야겠다.



### 웹개발 종합반 복습
스파르타피디아 프로젝트에서 ‘기록하기’버튼을 눌러서 만들어진 post-box에 ‘삭제’버튼을 만들어서 삭제하는 기능을 추가했다. 사전강의를 볼 때는 이해를 했지만 다시 혼자서 구현하려고 하니 헷갈려서 시간이 많이 걸렸다..

- 삭제버튼(스파르타피디아)
먼저 삭제 버튼을 만들고 버튼을 클릭했을 때 delete함수가 발생하도록 button태그를 html에서 추가해줬다. 그 다음에 key값을 만들어 주기 위해서 db list를 가져와서 변수에 할당해줬다.
```python
movie_list = list(db.movies.find({}, {'_id': False}))

key = 0
if len(movie_list) != 0:
    key = movie_list[len(movie_list) - 1]['key'] + 1
```

고유값을 주기 위해서 리스트의 길이를 사용했다. 리스트의 마지막 요소의 ‘key’값을 받아와서 +1을 해줘서 겹치지 않게 만들었다. 
```javascript
function del(key) {
    $.ajax({
        type: "POST",
        url: "/movies/del",
        data: {key_give:key},
        success: function (response) {
            alert(response["msg"])
            window.location.reload()
        }
    });
}
```
```python
@app.route("/bucket/del", methods=["POST"])
def bucket_del():
    key_receive = request.form['key_give']
    db.bucket.delete_one({'key':key_receive})
    return jsonify({'msg': '삭제 완료'})
```
삭제버튼을 눌렀을 때 실행되는 함수에 key를 전달해서 POST 메서드로 전달하고 db에서 key_receive값을 갖는 리스트를 삭제해주도록 했다. 

- 취소버튼(버킷리스트)

완료버튼을 눌렀을 때 완료했다고 줄이 그어지는데 완료된 리스트에 취소버튼을 추가해서 줄을 다시 없애보기로 했다. 삭제버튼을 만들었을 때와 비슷한데 update를 이용해서 구현해보았다.

리스트를 등록할 때 doc = {’done’ : 0} 을 넣어주고 완료가 되면 

`db.bucket.update_one({'num': int(num_receive)}, {'$set': {'done': 1}})`

를 써서 done값을 1로 업데이트 해줬다. 이때 데이터를 숫자가 문자열로 받아와져서 숫자로 바꿔줘야한다.

취소버튼을 누르면

`db.bucket.update_one({'key': int(key_receive)}, {'$set': {'done': 0}})`

다시 done값을 0으로 업데이트하면 된다.

알게된 점

배열에서 마지막 값을 가져오기 위해서 리스트의 길이에서 1을 뺀값을 이용했다.

`key = bucket_list[len(bucket_list) - 1]['key'] + 1`

len(bucket_list) - 1 대신에 -1만 넣으면 배열의 마지막값을 가리킨다는 것을 알게 되었다.

`key = bucket_list[- 1]['key'] + 1`

- 400error, 500error
    - 400 : Bad Request로써, 요청 실패-문법상 오류가 있어서 서버가 요청 사항을 이해하지 못함
        - front에서 문제가 발생했을 때
    - 500 : 서버 내부 오류는 웹 서버가 요청사항을 수행할 수 없을 경우에 발생함
        - back에서 문제가 발생했을 때


