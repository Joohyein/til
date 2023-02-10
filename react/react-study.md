## **Ducks pattern**

1. Reducer 함수를 `export default` 한다.
2. Action creator 함수들을 `export` 한다.
3. Action type은 `app/reducer/ACTION_TYPE` 형태로 작성한다.
    
    (외부 라이브러리로서 사용될 경우 또는 외부 라이브러리가 필요로 할 경우에는 UPPER_SNAKE_CASE로만 작성해도 괜찮다)
    

→ 모듈 파일 1개에 `Action Type` , `Action Creator` , `Reducer` 가 모두 존재하는 작성 방식이다.
