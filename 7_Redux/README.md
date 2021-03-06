# Ch 7. Redux 1

## 7-1. 개요
리액트로 금전출납부를 만들어보세요.
인풋창에 숫자를 입력하고 '입금' '출금'버튼을 누르면 각각 입/출금 현황 및 잔액이 표시되는 테이블을 구성하시면 되겠습니다. 디자인 필요없이 기능만 구현되면 되고, 서버에 저장하실 필요는 없습니다.

[ 숫자를 입력하세요(인풋) ] [입금(버튼)] [출금(버튼)]

| 입금 | 출금 | 잔액 |
| --- | --- | --- |
| 5000 | | 5000 |
| | 3000 | 2000 |

(기본방식으로 작성 후 리덕스로 전환한다).


## 7-2. 기본방식

```
- main
- App
  - InputBox     : input, buttons
  - AccountBook  : data table
```

## 7-3. Redux

https://dobbit.github.io/redux/

> 여러분의 앱의 상태 전부는 하나의 `스토어(store)`안에 있는 객체 트리에 저장됩니다.
>
> 상태 트리를 변경하는 유일한 방법은 무엇이 일어날지 서술하는 객체인 `액션(action)`을 보내는 것 뿐입니다.
>
> 액션이 상태 트리를 어떻게 변경할지 명시하기 위해 여러분은 `리듀서(reducers)`를 작성해야 합니다.
>
> 이게 다입니다!


### 7-3-1. Presentational component vs. Container component

기존 : https://dobbit.github.io/redux/basics/UsageWithReact.html#영민한smart-컴포넌트와-우직한dumb-컴포넌트

현재 :
http://redux.js.org/docs/basics/UsageWithReact.html#presentational-and-container-components
https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.5i4yjbprz

### 7-3-2. 구조

변경전

```
- main
- App
  - InputBox     : input, button['save'], button['withdraw']
  - AccountBook  : data table
```

변경후

```
- main
- store            : 모든 상태 정보를 저장하고 있는 저장소.
- [actions]        : 상태 변경을 위한 '명령' 기술
  - BankActions
- [containers]     : store에서 필요한 state들을 추출하여 props에 반영.
  - App
- [components]     : container에서 전달한 props들을 사용.
    - InputBox     : button 클릭시 select type과 input value를 토대로 액션 호출.
    - AccountBook
- [reducers]       : 실제 상태 변경을 수행하여 store를 갱신함.
  - BankReducer
```

### 7-3-3. 설치

```bash
> npm i -S redux react-redux
```

### 7-3-4. 기능추가
