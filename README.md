해당 저장소는 <a href="https://leafletjs.com/examples/quick-start/">Leaftlet JS</a> 공식 홈페이지를 참고하여 만들어졌음을 밝힙니다.

LeafLet JS는 지도를 웹 페이지에서 볼 수 있도록 도와주는 자바스크립트 라이브러리 입니다.

<img src="leafletJS_tutorial\gitImages\LeafLet_Logo.png">

## 페이지 준비

문서의 헤드라인에 CSS파일을 추가해줍니다.

```html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
   integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
   crossorigin=""/>
```

해당 link태그 바로 뒤에 스크립트 태그를 넣어줍니다 (반드시)

```html
 <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
   integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
   crossorigin=""></script>
```

이제 원하는 위치에 div태그를 만들어주면 준비가 완료됩니다.

```html
<div id="mapid"></div>
```

```css
#mapid { height: 180px; }
```

준비가 완료되었기에 지금부터 아래와 같은 지도를 만들어겠습니다.

<img src="gitImages\result_example.png">

```javascript
// 맵의 id는 mapid이며 처음에 보고있을 좌표와 높이를 설정합니다.
const mymap = L.map('mapid').setView([51.505, -0.09], 13)
```

이제 맵에 간단한 옵션만 주면 화면에 출력이 가능하다. 먼저, <a  href="https://account.mapbox.com/access-tokens/">홈페이지</a>에 가서 AccessToken을 발급받도록 하자

그 후 아래의 코드에 Token변수 대신 발급받은 토큰을 넣는다.

```javascript
L.tileLayer(`https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=${Token}`, {
   // 화면의 오른 쪽 하단에 글씨를 나타냄 HTML태그 사용이 가능함
   attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
   // 최대 줌
   maxZoom: 18,
   // 지도 종류
   id: 'mapbox/streets-v11',
   // 경로 사이즈
   tileSize: 512,
   // 현재 줌 
   zoomOffset: -1,
   // 발급받은 토큰
   accessToken: Token
}).addTo(mymap)
```

모두 완료한다면 아래와 같은 화면이 출력된다.

<img src="gitImages\draw_map.png">

### 마커 표시하기

마커를 표시하기위해 필요한 함수들은 이미 L이라는 내부객체에 선언되어있다.

```javascript
const marker = L.marker([51.5, -0.09]).addTo(mymap)
```

원형 마커는 아래와 같이 추가할 수 있다.

```javascript
const circle = L.circle([51.508, -0.11], {
   // 선 색
   color: 'red',
   // 채우기 색
   fillColor: '#f03',
   // 둥글기 정도
   radius: 500
}).addTo(mymap)
```

다각형 마커는 아래와 같이 추가할 수 있다.

```javascript
const polygon = L.polygon([
   [51.509, -0.08],
   [51.503, -0.06],
   [51.51, -0.047]
]).addTo(mymap)
```

다각형 마커의 각 배열 인자들은 꼭짓점의 좌표를 의미한다.

모두 완료한 경우의 결과화면은 아래와 같다.

<img src="gitImages\Shape.png">