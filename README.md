## 간단하게 Game Shop(임시)을 소개합니다.

### Ranun95.github.io  -크롬,엣지,웨일 로 테스트하였습니다.-

#### Game Shop(임시)sms 쇼핑몰의 형태로 현재는 게임판매를 주제로 제작되고 있지만 컨텐츠에 따라 내용물은 바뀔 수 있습니다.(물론 코드내 변수명도 바뀌겠지만)
#### JavaScript를 기반으로 React라이브러리를 이용해 제작중이며 Ajax를 이용해 외부 데이터 차후 DB와의 연동도 계획중입니다.

```javascript
let [games, gameschange] = useState(Data)
~
{ games.map((a,i)=>{
  return <Card games={games[i]} key={i}/>}
  )
}
~
function Card(props){
  return (
    <div className="col-md-4">
      <div className="col-md-4-img">
      <NavLink to={"/detail/"+props.games.id}>
        <img src={props.games.imgurl} width="100%" href="/"/>
      </NavLink>
        </div>
          <h5 className="col-md-4-title">{ props.games.title}</h5>
          <p>판매가 : { props.games.price} 원</p>
      </div>
  )
}
```
##### 상품에 대한 데이터를 받아 [games]라는 Array에 담았고 상품을 담을 Card라는 공간을 미리 만들어뒀습니다.이 Card공간의 생성은 상품 수에 따라 반복될것이기때문에 함수로 만들었고 Card라는 함수를 map이라는 반복문을 통해 앞으로 들어오는 데이터들을 반복적으로 같은 공간에 담아 생성되도록 만들었습니다.

```javascript
axios.get('https://ranun95.github.io/TestShop/data2.json')
     .then((result)=>{gameschange( [...games, ...result.data ])
                      console.log(result.data)
                     })
     .catch(()=>{console.log('실패.')
                })
```
##### axios를 이용 외부 데이터를 .get으로 받아와 [games]라는 Array에 담는걸로 했습니다. 그 과정에서 useState 함수의 배열은 직접 쓰는것보다 복사를 해서 사용하는게 좋다는 글을 보고
[...games]라는 복사본을 생성. [...result.data] 라는 받아온 데이터 또한 복사해서 gameschange라는 setState함수가 [games]의 값을 변경해줍니다.

```javascript
-App.js-
<Route path="/detail/:number"> 
        <Detail games={games} />
</Route>
-Detail.js
function Detail(props){
~
let {number} = useParams();
let SelGames = props.games.find(function(a){
        return a.id == number
```
##### 라우트를 이용해 상세페이지로 이동하게 만들었고 제품의 고유번호를 매개변수로 받고 그 번호와 일치하는 데이터들을 이후 상세페이지에 불러와 상품마다 상세페이지가 자동으로 만들어지게 만들었습니다.


##### JavaScript를 공부한지 얼마 되지 않았고 사이트도 1~2일정도에 만드느라 퀄리티가 낮은점 양해 부탁드립니다.

##### 추가 예정(개인기록) : DB연동(회원가입,로그인 기능) , 장바구니(가짜 구입기능) , 게시판 (자유) 등.
