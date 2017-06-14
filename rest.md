RESTful 웹 서비스
:	REST(REpresentation State Transfer)규정을 맞춰 만든 웹 서비스

이름 그대로 모든 요청에서 Client 의 상태(State) Representational 하게 전송합니다. Representational 하다는건, Client 의 요청이 URI 상에서 의미가 잘 드러난다는 뜻입니다.

~~~
http://example.com/cotnents?lists=3&id=1 //Non-RESTful URI 
http://example/com/contents/lists/3/id/1 //RESTful URI 
~~~


get
:	조회

post
:	추가

put
:	변경

delete
:	삭제


###Stateless

Stateless 하다는 것은 서버가 어떠한 Client 의 Status 도 저장하지 않는다는 뜻입니다. 따라서 Client 는 매 요청마다 자신을 인증할 수 있는 Token 이나 Key 등을 Request 에 포함시켜 전송합니다. 만약 클라이언트의 요청이 Stateful 하다면 서버가 클라이언트의 현재 상태를 저장해야하고, 클라이언트의 상태는 해당 서버에 종속이 됩니다. 만약 대규모 환경에서 동일한 웹서버를 다수 배치해 로드밸런싱을 하는 경우에 각 서버가 클라이언트의 상태, 세션을 공유할 수 있는 Redis 같은 별도의 시스템이 필요합니다. 그러나 Stateless 하다면 클라이언트의 요청은 어느 서버가 처리하던지 동일하게 처리할 수 있습니다. 클라이언트의 상태는 클라이언트의 요청 안에 모두 들어있으니까요.

###OAuth

OAuth 는 사용자(Resource Owner) 가 웹서비스(Client) 에게 로그인을 시도 했을때, 웹 서비스(Client) 가 페이스북(Auth Server) 에게 인증을 받아 적절한 권한이 부여된 Token 을 얻은 뒤, 필요한 사용자의 정보(프로필 이미지, 출신 학교) 등등을 페이스북(Resource Server) 에서 권한 확인 후 얻어오는걸 말합니다. 이미지로 보시는게 훠어어어얼씬 이해가 빠르겠습니다. OAuth 에 대해선 다음 챕터에서 다룰 것이므로 이만 줄이겠습니다. 더 자세한 내용은 OAUTH 2.0 – OPEN API 인증을 위한 만능 도구상자



출처: http://anster.tistory.com/163 [Old Lisper]
