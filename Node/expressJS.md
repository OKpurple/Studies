###Node.js 서버 실행 코드

~~~
//모듈 추출
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

//서버 생성 'function(){}' == '=>'
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

//서버 실행
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
~~~

###Express

~~~
// expres 모듈추출
var express = require('express');

// 서버 생성
var app = express();

// request 이벤트 리스너 연결 (이러한 함수를 미들웨어)
app.use(function(req, res, next)) {
}

// 서버 실행
app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
~~~

###라우터 미들웨어

~~~
// 라우터 미들웨어의 get(path, callback[, callback ...])
app.get('/', function (req, res) {
  res.send('Hello World!');
});	//post, put, delete, all
~~~

params
: ':'기호를 사용해 지정된 라우팅 변수

query
: ?name=A와 같은 요청 매개변수

~~~
app.get(/page/:id, function(req,res){
	res.send(request.params.id);
});
~~~

###static 미들웨어
~~~
//파일 제공
app.use(express.static(__dirname + '/public'));
~~~

###cookie parser 미들웨어
요청 쿠키를 추출

npm install cookie-parser

~~~
app.use(cookieParser());

...
//쿠키를 생성
response.cookie('string', 'cookie');
response.cookie('json',{
	name: 'cookie',
	property: 'delicious'
});

// 응답
response.send(request.cookies);
~~~

###body parser 미들웨어
post요청 데이터를 추출

npm install body-parser

~~~
app.use(bodyParser,urlencoded({extended: false}));
~~~

###express-session 미들웨어
서버에 별도저장소에 데이터를 저장

npm install express-session

~~~
app.use(session({
	secret: 'secret key',
	resave: false,
	saveUninitialized: true
}));
~~~

~~~
//세션을 저장
reqeust.session.now = (new Date()).toUTCString();
//응답
response.send(request.session);
~~~
express 모듈이 훨씬 많은 기능이 있음