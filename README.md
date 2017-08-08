# Portfolio

이 페이지에서는 제가 개인적으로 프로젝트 중에서 상대적으로 큰 프로젝트들을 모아 설명하고 있습니다. 대부분의 소스는 GitHub에 공개되어 있습니다.

## Ability

아래 목록에 있는 기술들을 사용하여 하나 이상의 프로젝트를 진행해 본 적이 있으며, 자주 사용하는 순서대로 나열했습니다.

- Language
  - Go
  - Javascript / node.js / HTML / CSS
  - C/C++
  - Java
- Framework / Toolkit
  - [Polymer](https://www.polymer-project.org/)
  - [Angular](https://angular.io/)
- Environment
  - Google Cloud Compute
  - Amazon Web Service
  - Heroku
  - Docker

***

## Table of Contents

- [ourChess (2012)](https://github.com/geeksbaek/portfolio#ourchess-2012)
- [Project Arche (2014~2017)](https://github.com/geeksbaek/portfolio#project-arche-2014)
- [goinside (2016~)](https://github.com/geeksbaek/portfolio#goinside-2016)

## [ourChess](https://github.com/geeksbaek/ourChess) (2012)

#### Summary

ourChess는 웹 기반으로 개발된 멀티플레이어 1:1 체스게임입니다. Backend는 [node.js](https://nodejs.org/), Frontend는 Javascript와 약간의 [jQuery](https://jquery.com/)를 사용하여 개발했으며, HTML5 Canvas API로 2D 이미지를 그려 그래픽을 구현하였습니다. UI는 [Bootstrap](http://getbootstrap.com/)을 사용하여 구성하였으며, 사용자들은 [Socket.io](https://socket.io/)의 websocket으로 서로 실시간으로 통신합니다. 현재 [Heroku](https://www.heroku.com/)에서 서비스 중입니다.

#### Details

멀티플레이어 게임이므로, 사용자들은 각자 방을 생성하여 동시에 게임을 플레이할 수 있습니다. socket.io가 서버에 연결된 소켓들을 네임스페이스로 구분하는 기능을 지원하는 덕분에 방을 쉽게 구현할 수 있었습니다. 방을 생성하면 랜덤한 문자열이 생성되는데, 이 문자열을 네임스페이스로 사용하여 방을 구분짓습니다.

개발에서 중요하게 생각한 부분은 멀티스크린을 지원하는 것이었습니다. 제가 웹 기반 어플리케이션을 좋아하는 이유는 웹이 플랫폼으로서 주는 이점이 상당하기 때문입니다. 해상도가 변경되면 화면 방향을 계산한 뒤 UI를 재배치하여 모바일 환경에서도 자연스럽게 보이도록 하였습니다.

<p align="center">
  <img src="http://i.imgur.com/XhWvXj2.png" width="170"> <img src="http://i.imgur.com/M5uApvG.png" width="170">
</p>

이 체스 게임의 주요 특징은 플레이어가 기물을 움직이는 모습을 다른 플레이어들이 실시간으로 볼 수 있다는 것입니다. 이를 자연스럽게 구현하기 위해 크게 두 가지 테크닉을 사용했습니다.

첫째, 체스판 위에서 기물을 드래그하는 동안 마우스 좌표를 실시간으로 websocket을 통해 브로드캐스트합니다. *(현재 [코드](https://github.com/geeksbaek/ourChess/blob/heroku/public/js/dragAndDrop.js#L2) 상에서는 mousemove 이벤트가 발생했을 때 좌표 브로드캐스트 하도록 되어있는데, 지금 생각해보니 mousemove 이벤트 대신 mousedown, mouseup 이벤트로 브로드캐스트 코드를 실행하는 setInterval 함수를 동적으로 생성 및 파괴하는 방식으로 구현하는 것이 더 나아 보입니다. mousemove 이벤트는 초당 60번을 초과할 수 있는데, 그렇게 자주 브로드캐스트 하는 것은 낭비라고 생각됩니다.)*

둘째, 좌표를 브로드캐스트 받은 클라이언트들은 기물이 움직이는 것을 구현하기 위해 Canvas를 다시 그려야 합니다. 이때, 체스 보드가 그려져 있는 메인 Canvas를 다시 그리는 대신 별도의 Canvas를 생성하여 이곳에 움직일 기물을 그린 뒤, CSS Position을 변경하여 움직이도록 합니다. Canvas를 초당 60번씩이나 다시 그리는 것은 비효율적일뿐더러 그래픽 또한 부자연스럽게 보이기 때문에 이 트릭을 사용하였습니다.

<p align="center">
  <img src="http://i.imgur.com/zqpfsa5.gif" width="400">
</p>

#### Story

온라인 멀티플레이어 체스 게임을 만들기로 한 뒤, 제가 가장 중요하게 생각한 목표는 "비록 컴퓨터를 사이에 놓고 두는 체스지만, 진짜 사람과 두는 기분을 들게 하자" 였습니다. 어떻게 해야 그런 기분을 들게 할 수 있을지 고민한 끝에, 상대가 기물을 움직이는 모습을 실시간으로 보여주면 좋을 것 같았습니다. 이 아이디어를 실현하기 위해 많은 시행착오를 거치면서 기술을 개선한 끝에 만족스러운 결과를 얻게 되었습니다.

개발에서 시간이 가장 많이 들어간 부분은 기물의 움직임이 체스의 규칙을 위반하는지 검사하는 [코드](https://github.com/geeksbaek/ourChess/blob/heroku/public/js/checkAvailability.js)를 작성하는 부분이었습니다. Stalemate, Threefold repetition, Promotion 등 대부분의 체스 규칙을 검사하며, 규칙에 위반되는 움직임은 허용되지 않도록 하였습니다. 사실 이 부분은 서버에서 검사해야 하지만, 개발 편의상 클라이언트에서 검사하게 했습니다. 만약 제대로 서비스해야 한다면 이러한 부분은 보완을 거쳐야 합니다.

이 어플리케이션은 제가 처음으로 개발한 프로그램이어서 의미가 남다릅니다. 대학교 1학년을 마친 뒤 군 휴학 중에 한 달동안 집에 틀어박혀서 개발했는데, 질문을 하거나 조언을 구할 사람이 없었기 때문에 모든 것을 혼자서 찾아 배워야 했습니다. 이 과정 속에서 스스로 문제를 해결하는 능력을 기르고, 혼자서도 하나의 프로젝트를 완성할 수 있다는 자신감을 얻었습니다.

#### Usage

[여기](https://ourchess.herokuapp.com/)에서 직접 플레이해보실 수 있습니다.

***

## Project Arche (2014~2017)

Project Arche는 [아키에이지](http://archeage.xlgames.com/)라는 MMORPG 사용자들에게 도움을 주기 위해 개발한 어플리케이션입니다. 지금은 서비스가 중지된 웹 어플리케이션 버전과 현재 서비스되고 있는 REST API 버전으로 나누어져 있습니다.

## [웹 어플리케이션 버전](https://github.com/geeksbaek/Project-Arche) (2014~2015)

#### Summary

웹 어플리케이션 버전의 Project Arche는 [아키에이지](http://archeage.xlgames.com/)라는 MMORPG에 관한 통계 데이터를 제공하는 서비스입니다. Backend는 Javascript와 유사한 문법을 사용하는 [Google Apps Script](https://developers.google.com/apps-script/)로 개발하였고, [Google App Engine](https://cloud.google.com/appengine/)에서 호스팅됩니다. [Google Spreadsheets](https://www.google.com/sheets/about/)를 Database처럼 사용합니다. Frontend는 [Polymer](https://www.polymer-project.org/)를 사용하여 Single Page App으로 개발하였습니다.

#### Details

통계를 내기 위해 정기적으로 Google Apps Script (이하 GAS) 에서 웹 크롤링 및 파싱을 수행합니다. GAS는 urlFetch라는 API로 HTTP 통신이 가능하므로 크롤링이 가능합니다. 하지만 jQuery 같은 외부 자바스크립트 라이브러리를 사용하기 어렵기 때문에 주로 정규 표현식으로 데이터를 파싱했습니다. 

파싱된 데이터는 타임스탬프와 함께 Google Spreadsheets에 저장합니다. GAS에서 Spreadsheets에 접근하는 API를 제공했고, 저장할 데이터 양도 크기 않았기 때문에 데이터베이스로 Spreadsheets를 선택한 것은 나쁘지 않은 선택이었습니다. 

Frontend는 [Google Charts](https://developers.google.com/chart/) 라이브러리를 통해 해당 Spreadsheets의 데이터를 사용자들에게 보여줍니다. UI는 Polymer에서 제공하는 머터리얼 디자인으로 만들어진 컴포넌트들을 사용하여 구성했습니다.

<p align="center">
  <img src="http://i.imgur.com/hvVFxEz.gif" width="300"> <img src="http://i.imgur.com/YzLMsAp.gif"  width="300">
</p>

#### Story

개발을 시작할 당시 아키에이지는 꽤 인기 있는 게임이었습니다. 세력 간 대립이 주요 컨텐츠였기 때문에 어떤 세력이 더 강한지, 어떤 세력이 성장하고 있는지가 플레이어들에게 중요한 이슈였습니다. 게임사에서 공식적으로 통계를 내주진 않았으나 각 길드의 정보는 홈페이지에서 제공되었으므로 사용자가 임의로 통계를 내는 것은 가능했기 때문에 이 어플리케이션을 개발하게 되었습니다.

사실 GAS는 웹 크롤링같은 긴 시간 동작하는 프로그램을 위해 적합한 솔루션이 아닙니다. GAS는 작업이 함수 단위로 나누어져 있는데, 단일 함수의 최대 실행시간이 [6분](https://stackoverflow.com/a/29800759) 밖에 되지 않습니다. 가뜩이나 느린 urlFetch 요청을 GAS 특성상 비동기적으로 작성할 수도 없어서 웹 크롤링을 하기에는 장애물이 많았습니다.

하지만 아키에이지 플레이 시간을 쪼개가면서 다른 솔루션을 배워 마이그레이션하기에는 시간이 부족했으므로, GAS 내에서 해결하는 방법을 찾아야 했습니다. 고민 끝에 함수의 실행시간을 측정하다가 6분을 초과하기 전에 작업을 중간 저장하고, 잠시 후에 다시 함수가 다시 실행되도록 하였습니다. 이 작업을 반복하는 방법으로 매일 거의 반나절 이상 크롤러가 돌아가게 되었으나, 다행히 무료 할당량을 초과하지 않았고 모든 작업이 자동으로 이루어졌으므로 결국 이 구조로 서비스가 종료될 때까지 유지되었습니다.

서비스가 종료된 이유는, 모든 게임이 그렇듯 인기가 점점 시들었기 때문입니다. 아키에이지의 인기가 떨어진 이유로 서버 내 세력 간의 균형이 무너진 것도 한 몫을 했는데, 세력의 힘을 가늠하기 위해 제공했던 이 통계가 이젠 플레이어들에게 큰 의미가 없다고 판단했습니다.

#### Usage

이 어플리케이션은 지금은 서비스되고 있지 않습니다. 대신 [동영상](https://www.youtube.com/watch?v=k35ciJNoqR0)으로 체험하실 수 있습니다.

## REST API 버전 (2017)

#### Summary

REST API 버전의 Project Arche는 아키에이지 공식 홈페이지에서 제공하는 정보들을 JSON 포맷으로 파싱해주는 서비스입니다. 또한 [Discord](https://discordapp.com/)와 [Webhook](https://en.wikipedia.org/wiki/Webhook)으로 연동한 [아키에이지 알림 서비스](https://goo.gl/forms/AovCs0Au1C0TfcDB3)도 제공하고 있습니다. [Golang](https://golang.org/)으로 개발되어 현재 [Google App Engine](https://cloud.google.com/appengine/)에서 서비스되고 있습니다. [gorilla/mux](https://github.com/gorilla/mux) 라이브러리를 사용하여 각 요청을 라우팅합니다. Database는 [Google Cloud Datastore](https://cloud.google.com/datastore/)를 사용합니다.

※ REST API 서버의 전체 소스는 인증에 사용되는 클라이언트 ID, 비밀키 등이 포함되어 있으므로 공개하지 않습니다.

#### Details

이 서버는 크게 두 가지 서비스를 제공합니다.

1. REST API 서비스

```
GET https://project-arche.appspot.com/api/auctions/{server_group}/{item_name}
GET https://project-arche.appspot.com/api/notices
GET https://project-arche.appspot.com/api/serverStatus
```

위 양식대로 REST API를 제공하고 있습니다. 공개 사용을 위해 만들었기 때문에 별도의 인증 없이 사용할 수 있습니다. 해당 요청을 받은 서버는 [archeage-go](https://github.com/geeksbaek/archeage-go) 라이브러리를 사용하여 아키에이지 공식 홈페이지에서 데이터를 가져옵니다. 이 라이브러리는 Project-Arche 소스코드의 관리를 위해 파싱 부분을 별도의 패키지로 분리한 것입니다. 파싱을 위해 jQuery와 유사한 [goquery](https://github.com/PuerkitoBio/goquery) 라이브러리를 사용하였습니다.

요청이 너무 많아지면 Project-Arche 서버 뿐 아니라 아키에이지 공식 홈페이지에까지 부담을 줄 수가 있으므로, 실제 데이터는 주기적으로 실행되는 cron 작업에 의해서만 가져오도록 했으며 일반적은 요청은 cron 작업에 의해 캐시된 데이터를 반환합니다. 캐시를 보관하기에 적절한 Memcache라는 서비스가 존재하지만, Memcache는 과금을 하지 않으면 안전성이 보장되지 않기 때문에 대신 Datastore라는 NoSQL Database에 캐시하도록 하였습니다.

2. 알림 구독 서비스

공식 홈페이지에 새 공지사항이 올라오거나 게임 서버 상태가 변경되면 구독자들에게 알려주는 서비스를 제공합니다. cron 작업이 주기적으로 공식 홈페이지를 체크하다가, 변경 사항이 발생하면 미리 등록된 알림 구독자들에게 Webhook으로 메시지를 보냅니다. 현재는 Discord라는 게이머 전용 메신저와 연동을 지원합니다.

Google Form을 통해 알림 구독을 [신청](https://goo.gl/gVntmm) 받으며, 구독자 정보는 자동으로 Google Spreadsheets에 저장됩니다. 알림을 보낼 때 마다 이 Spreadsheets를 조회하여 Webhook을 보냅니다. 이 Spreadsheets에 접근 인증을 받기 위해 Google Cloud Console에서 발급받은 JWT 토큰을 사용하는데, 이 토큰 때문에 GitHub가 아닌 Google의 Private Repository에서 소스를 관리하고 있습니다.

아래는 현재 서비스되고 있는 Project-Arche 서버의 상태 그래프입니다. 오랜 기간동안 안정적으로 서비스되고 있는 모습입니다.

<p align="center">
  <img src="http://i.imgur.com/BGZvYgF.png">
</p>

#### Story

학업에 열중하기 위해 잠시 아키에이지를 접었다가, 새로운 서버가 나온다는 소식에 다시 게임을 시작하면서 이 서비스를 개발했습니다. 애초에 이 REST API는 훨씬 더 많은 정보를 제공하도록 할 예정이었으나, 아키에이지의 인기가 빠르게 다시 식어버리자 저의 개발에 대한 의지도 같이 식어버리고 말았습니다. 이미 개발한 서비스는 무료 할당량 내에서 계속 서비스하고 있습니다.

#### Usage

REST API 서비스와 이 API를 이용해서 시범적으로 만든 서비스를 [공개](http://www.inven.co.kr/board/powerbbs.php?come_idx=2641&l=12554)하고 많은 플레이어들이 관심을 가져 주었습니다. 몇몇 분들은 제 REST API 서버를 이용하여 새로운 서비스를 만들어 [배포](http://www.inven.co.kr/board/powerbbs.php?name=subjcont&keyword=l%3D12554&x=29&y=4&come_idx=2641&iskin=&mskin=&p=1&query=list&my=&category=&sort=PID&orderby=&sterm=)하기도 했습니다. 알림 구독 서비스 또한 [공개](http://www.inven.co.kr/board/powerbbs.php?come_idx=2641&l=12839)한 이후로 수 십개의 Discord에서 이 서비스를 구독하고 있습니다.

***

## [goinside](https://github.com/geeksbaek/goinside) (2016~)

#### Summary

goinside는 디시인사이드 포털에서의 행동을 Go로 구현한 API 패키지입니다. 초기에는 웹 페이지를 일일이 파싱하여 기능을 구현했으나, 디시인사이드 앱에서 사용하는 비공개 REST API를 발견하여 현재는 디시인사이드 비공개 REST API의 래퍼 라이브러리 형태를 띄고 있습니다.

goinside는 제가 지금까지 개발한 라이브러리 중에서 가장 규모가 큰 라이브러리입니다. 최대한 많은 기능을 지원하기 위해 노력했고, 디시인사이드 비공개 REST API에서 지원하지 않는 갤로그 관련 기능도 일부 [구현](https://github.com/geeksbaek/goinside/tree/master/gallog)했습니다. Go 언어를 최대한 이용하여 간결하고 유연하게 설계했으며 대부분의 함수를 커버하는 테스트 코드를 작성하여 유지 보수에 신경썼습니다. [API 문서](https://godoc.org/github.com/geeksbaek/goinside) 또한 신경써서 작성하였습니다.

#### Details

디시인사이드 비공개 REST API를 래핑하기 위해서 우선 해당 API의 사용 방법을 정확히 익혀야 했습니다. 이 API에 대한 문서같은 것은 존재하지 않았기 때문에, 서버와 앱이 통신하는 패킷을 분석하고 앱 자체를 디컴파일해서 분석하는 방법을 사용했습니다. 앱은 난독화가 되어있었기 때문에 분석이 쉽지는 않았습니다.

분석 결과, 서버와 [이상한 방식](https://github.com/geeksbaek/goinside/issues/6)으로 통신한다는 것을 알아낼 수 있었습니다. 비공개 REST API와의 모든 통신은 다음 과정을 거칩니다.

1. 정상적인 URL를 그대로 요청하지 않고 파라메터 부분을 Base64로 인코딩합니다.
2. 인코딩한 값을 hash라는 이름의 파라메터에 넣어 redirect.php로 요청을 보냅니다.
3. 요청을 받은 서버는 정상적인 파라메터 뒤에 서버에서 생성한 것으로 추정되는 hash라는 파라메터가 추가된 URL로 Redirect 합니다.
4. Redirect된 요청에서 정상적인 응답이 반환됩니다.

이 작업이 무슨 의미가 있는 지 알 수 없으나, 이 API를 사용하기 위해선 이 방법을 따라야 했으므로 똑같이 구현하는 수 밖에 없었습니다. [이 부분](https://github.com/geeksbaek/goinside/blob/master/request.go#L32-L53)과 [이 부분](https://github.com/geeksbaek/goinside/blob/master/request.go#L129-L134)이 해당 작업을 Go로 구현한 부분입니다.

그 외에 기본적인 기능들을 래핑하는 것은 어렵지 않았습니다. 다만, 갤로그에 대해서는 비공개 API가 존재하지 않았기 때문에 [goinside/gallog](https://godoc.org/github.com/geeksbaek/goinside/gallog) 라는 이름의 서브 패키지에서 웹 파싱을 통해 기능을 [구현](https://github.com/geeksbaek/goinside/blob/master/gallog/gallog.go)했습니다.

goinside/gallog 에는 [Session.FetchAll](https://godoc.org/github.com/geeksbaek/goinside/gallog#Session.FetchAll), [Session.DeleteAll](https://godoc.org/github.com/geeksbaek/goinside/gallog#Session.DeleteAll)과 같은 대량 HTTP 작업을 수행하는 함수가 있습니다. Go가 동시성을 잘 지원하는 덕분에 이런 대량 HTTP 작업들을 동시적으로 빠르게 처리하도록 [구현](https://github.com/geeksbaek/goinside/blob/master/gallog/gallog.go#L205-L249)할 수 있었습니다. 매 요청을 별도의 Goroutine에서 수행하도록 하여 비차단식으로 작동하며, 동시에 너무 많은 Gorountine이 생성되지 않도록 제한을 걸어두었습니다.

현재 테스트 코드의 커버리지는 약 60%이며, 지속적으로 코드의 안정성을 개선하고 있습니다. (travis 빌드 도구를 통해 측정된 커버리지는 로컬에서만 수행할 수 있는 일부 테스트 코드를 주석처리 했기 때문에 정확하지 않습니다.)

```
PS C:\Users\geeks\Documents\github\goinside> go test -cover
PASS
coverage: 59.3% of statements
ok      _/C_/Users/geeks/Documents/github/goinside      8.424s
```

#### Story

사실 이 라이브러리는 아래에서 설명해 드릴 [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner)라는 프로그램을 만들다가 점점 커지는 코드를 용이하게 관리하기 위해 분리한 것입니다. API 라이브러리를 만들어 두면 봇을 만드는데 사용하는 등 여러모로 쓸모가 있을거라고 생각했습니다. 이 라이브러리로 제작한 [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler)라는 이미지 수집 프로그램도 있습니다.

처음에는 실제 디시인사이드 웹사이트의 요청 방식을 모방하여 API를 구현했습니다. 이 방식은 웹사이트 구조가 바뀌면 그때마다 다시 웹사이트를 다시 분석하여 코드를 수정해야 하는 문제가 있습니다. 웹사이트 구조가 바뀌는 일은 비일비재하므로 그다지 좋은 방법은 아니었습니다. 이후에 디시인사이드 어플리케이션에서 비공개 내부 REST API 서버와 통신하는 것을 발견했고, 대대적으로 코드를 개선하면서 성능이 상당히 개선되었습니다.

#### Usage

- [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler)

goinside-image-crawler는 디시인사이드에 게시되는 글에서 이미지를 수집하는 프로그램입니다. 

익명의 요청을 받아 개발했습니다. 여러 개의 이미지를 동시적으로 내려받으며, 이미지 중복 검사 기능이 있어 중복된 이미지는 내려받지 않습니다. 현재는 [이슈](https://github.com/geeksbaek/goinside/issues/9)가 있어 정상적으로 동작하지 않습니다.

- [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner)

goinside-gallog-cleaner는 일명 디시 클리너라고 불리는 프로그램입니다. 회원으로 작성한 모든 글과 댓글을 삭제해줍니다.

디시인사이드에는 자신의 글을 일괄 삭제하는 기능이 없기 때문에 이런 작업을 대신 해주는 프로그램에 대한 수요가 항상 있어왔습니다. 과거부터 수 많은 디시 클리너들이 있었지만 지금은 모두 사용이 막힌 상태이기 때문에 누군가 새로운 디시 클리너를 만들어야 했습니다. 정작 저는 디시인사이드 회원이 아니기 때문에 사용하지 않는 프로그램이지만, 다른 많은 사용자들을 위해 지속적으로 관리하고 있습니다. 현재 누적 다운로드 1.4만번을 기록할 정도로 인기있는 프로그램입니다.