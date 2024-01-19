# 제목1

## 제목2

### 제목3

#### 제목4

##### 제목5

###### 제목6

  

글자 크기를 바꾸는 것이 아닌 제목을 구분하기 위해 사용

  

- bullet point

- 순서가 없음

1. 순서가 있는

2. list

    - 내부 리스트

        - 의 내부 리스트

  

## 코드가 여러줄일때

```javascript

const getLotto = function () {

  axios({

    url: 'http://127.0.0.1:5000/lotto'

  })

    .then(function (res) {

    console.log(res.data)

    addChat('receive', res.data)

    })

    .catch(function (err) {

    console.log(err)

    })

}

```

  

## 코드가 한줄일때

`console.log(res.data)`

  

## 하이퍼링크

[에듀싸피](https://edu.ssafy.com/edu/main/index.do)

  

## 이미지

  

- 로컬이미지 넣어보기

![픽셀하트](giphy.gif)

	 - 마크다운 파일을 옮길 때 로컬 이미지도 같이 옮겨야 함!!

  

- 인터넷이미지 넣어보기

![snowman](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSI3MkT7ZdBXzqvb_r7iSO2zskEYLduqwAOxJKFCqdaz8aDJvcSJmCBuV2GsNle0OKA4Gs&usqp=CAU)

  

## 텍스트 관련 문법

- 굵게(앞뒤로 **)

    : **안녕하세요**

- 기울이기(앞뒤로 *)

    : *안녕하세요*

- 취소선(앞뒤로 ~~)

    : ~~안녕하세요~~

  

## 수평선(구분선)

-(hypen) 3개 이상 적으면 작동

  

---

---

## 인용문 작성하기
'>' + 문장
> 이렇게 작성하면 인용문 형태
>>인용문 내부에도

## 테이블 작성

| 이름 | 반 |  |  |
| ---- | ---- | ---- | ---- |
| 김싸피 | 서울1반 |  |  |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
## Markdown Guide

[Markdown Guide](https://www.markdownguide.org/)