### nextjs introduction

### 프레임 워크와 라이브러리 의 차이.

```

```

### preRendering

```
앱 내에 있는 페이지들을 미리 랜더링 한다는것.
Cra ( create-react-app) 과 next 의 가장 큰 차이점 중 하나가 PreRendering 이다.
cra 로 작성된 화면을 확인할시. js 가 없으면 ui 를 그릴수 없는것을 확인 할 수 있다.

개발자 도구를 켜서 cra 페이지를 확인하면 , <div id="root"></div> 외에 전부 자바스크립트 인 것을 확인 할 수 있다.
크롬에서 js 를 비활성화 하는 체크란이 있는데 체크시
cra 로 작성된 화면에서 뭐라고 노출 되냐면.
You need to Enable Javascript to run this App 이라는 문구가 노출된다.
( 이유는 간단하다. 자바스크립트가 활성화 되지 않았고 이 앱이 실행되려면, 자바스크립트가 필요하기 떄문이다.)
반면 Next 는 어떨까.
이미 "어떨까" 라는 대목에서 눈치챘겠지만. HTML 을 모두 그려온다.
적어도 "유저가 HTML 은 볼 수 있다는 얘기" 고.
유저는 API 만 기다리면 된다는 이야기 이다.

예를들어 넷플릭스가 CRA 로 구성되어 있고 인터넷이 아주아주 느린 상황에서 어떻게되는지 CRA부터 확인해보자.

넷플릭스 -> CRA라면 ? (환경 :필리핀)

유저가 넷플릭스 들어오는 순간

흰화면이 제일먼저 노출되고 DOM 이 차근차근 그려지면서 API 도 기다리고있다.
마치 밥 아저씨가 생 도화지에다 그림을 4 배속으로 그리고 있는것 처럼.
이유는 JS 가 DOM 을 그리고 있기 때문이다.

반면 NEXT 는 어떨까.
이미 그려져있고 API만 기다리면 되는 상황에 있다.
밥 아저씨가 이미 다 그려놓은 그림에 우리는 API 만 기다리면 되는 상황이라고 비유 하는것이 이해가 되겠는가.
```

### next js 에서 nav 태그에 무지성으로 a 태그를 쓰면 안되는이유.

```
결과 부터 말하자면 새로고침 때문이다.
새로 그리기때문에 느릴것으로
nextjs 에서는 Link 컴포넌트에 감싸주면 된다.
<Link href="/"><a>홈으로 꺼저.</a></Link>
위와 같이 사용권장.

추가로 개발자도구로 inspect 확인할때. html 에선 <nav><a>홈으로 꺼저.</a></nav> 로
보일 것이다. 이게 뭘 의미하냐면 코드레벨에서 <Link> 태그에 속성을 추가 할 수 없다는 의미이다.
style 등등
그래서 <a> 태그에 속성을 넣어주고 Link 태그에는 단순히 href 경로만 넣어주면 된다.
```

### next 에서 style 적용하는 방법

```
기존에 알고있던 방법 2 가지
style={{}} // inline 스타일 박는법
css 파일에 class 작성후 import ./내가 만든css 파일

style 을 적용하려던 태그에 className="내가만든class"

새로 알게된 2가지
1. css module 패턴. -> [file].module.css
먼저 불러와주고
import styles from [file].module.css

className={styles.클래스네임}
조건 부 style 작성시 className={`${style.클래스네임} 조건 ? ${style.클래스네임} : '' `}
배열로 풀어내고 싶은 경우 className={`[ ${style.클래스네임} , 조건 ? ${style.클래스네임 } : '' ].join(" ")`}

2. styled jsx (next 고유의 방법) 주의 ( 해당 컴포넌트에서만 scope 를 갖는다)
<style jsx>{`
 a {
     text-decoration: none;
 }
 nav {
     background-color: tomato;
 }
`}
<style>

```
