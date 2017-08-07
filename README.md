# Portfolio

이 페이지에서는 제가 개인적으로 프로젝트 중에서 상대적으로 큰 프로젝트들을 모아 설명하고 있습니다. 대부분의 소스는 GitHub에 공개되어 있습니다.

## Ability

저는 아래 목록에 있는 기술들을 사용하여 프로젝트를 진행해 본 적이 있습니다. 자주 사용하는 순서대로 나열했습니다.

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
- [Project Arche (2014~)](https://github.com/geeksbaek/portfolio#project-arche-2014)
- [Joongbu Web App (2016~2017)](https://github.com/geeksbaek/portfolio#joongbu-web-app-20162017)
- [goinside (2016~)](https://github.com/geeksbaek/portfolio#goinside-2016)

## [ourChess](https://github.com/geeksbaek/ourChess) (2012)

<img src="http://i.imgur.com/zqpfsa5.gif" width="500">

#### Summary

ourChess는 웹 기반으로 개발된 1:1 체스게임입니다. backend는 [node.js](https://nodejs.org/), frontend는 Javascript와 약간의 [jQuery](https://jquery.com/)를 사용하여 개발했으며, HTML5 Canvas API로 2D 이미지를 그려 그래픽을 구현하였습니다. UI는 [Bootstrap](http://getbootstrap.com/)을 사용하여 구성하였으며, 사용자들은 [Socket.io](https://socket.io/)의 websocket으로 서로 실시간으로 통신합니다. 현재 [Heroku](https://www.heroku.com/)에서 서비스 중입니다.

#### Details

이 체스게임의 주요 특징은 플레이어가 기물을 움직이는 모습을 다른 플레이어들이 실시간으로 볼 수 있다는 것입니다. 이를 자연스럽게 구현하기 위해 크게 두 가지 테크닉을 사용했습니다.

- 첫째, 체스판 위에서 기물을 드래그하는 동안 마우스 좌표를 실시간으로 websocket을 통해 브로드캐스트합니다. 구체적으로는 초당 최대 60번까지 브로드캐스트합니다. 드래그 중에 발생하는 mousemove 이벤트는 초당 60번을 초과하여 발생할 수 있으므로, mousemove 이벤트 리스너를 사용하는 대신 setInterval 함수를 동적으로 생성하고 파괴하는 방법을 사용합니다.

- 둘째, 좌표를 브로드캐스트 받은 클라이언트들은 기물이 움직이는 것을 구현하기 위해 Canvas를 다시 그려야 합니다. 이때, 체스 보드가 그려져 있는 메인 Canvas를 다시 그리는 대신 별도의 Canvas를 생성하여 이곳에 움직일 기물을 그린 뒤, CSS Position을 변경하여 움직이도록 합니다. Canvas를 초당 60번씩이나 다시 그리는 것은 비효율적일뿐더러 그래픽 또한 부자연스럽게 보이기 때문에 이 트릭을 사용하였습니다.

#### Story

온라인 멀티플레이어 체스 게임을 만들기로 한 뒤, 제가 가장 중요하게 생각한 목표는 "비록 컴퓨터를 사이에 놓고 두는 체스지만, 진짜 사람과 두는 기분을 들게 하자" 였습니다. 어떻게 해야 그런 기분을 들게 할 수 있을지 고민한 끝에, 상대가 기물을 움직이는 모습을 실시간으로 보여주면 좋을 것 같았습니다. 이 아이디어를 실현하기 위해 많은 시행착오를 거치면서 기술을 개선한 끝에 만족스러운 결과를 얻게 되었습니다.

개발에서 시간이 가장 많이 들어간 부분은 기물의 움직임이 체스의 규칙을 위반하는지 검사하는 [부분](https://github.com/geeksbaek/ourChess/blob/heroku/public/js/checkAvailability.js)이었습니다. [Stalemate](https://en.wikipedia.org/wiki/Stalemate), [Threefold repetition](https://en.wikipedia.org/wiki/Threefold_repetition), [Promotion](https://en.wikipedia.org/wiki/Promotion_(chess)) 등 대부분의 체스 규칙을 검사하며, 규칙에 위반되는 움직임은 허용되지 않도록 하였습니다.

이 어플리케이션은 제가 처음으로 개발한 프로그램이어서 의미가 남다릅니다. 대학교 1학년을 마친 뒤 군 휴학 중에 한 달동안 집에 틀어박혀서 개발했는데, 질문을 하거나 조언을 구할 사람이 없었기 때문에 모든 것을 혼자서 찾아 배워야 했습니다. 이 과정 속에서 혼자서도 할 수 있다는 자신감을 얻었습니다.

#### Usage

[여기](https://ourchess.herokuapp.com/)에서 플레이해보실 수 있습니다. 방을 생성하면 고유 URL을 할당받는데, 이 URL을 공유하여 다른 사용자가 입장하면 자동으로 게임이 시작됩니다. 방을 생성한 사람이 White를 잡고, 다음으로 입장한 사람이 Black을 잡습니다. 이후에 입장한 사람들은 관전자가 됩니다. 체스 보드 옆에는 게임 메시지 수신 및 채팅을 할 수 있는 공간이 있습니다.

***

## Project Arche (2014~)

Project Arche는 두 가지 버전이 있습니다.

### [웹 어플리케이션 버전](https://github.com/geeksbaek/Project-Arche) (2014~2015)

<img src="http://i.imgur.com/hvVFxEz.gif" width="250"> <img src="http://i.imgur.com/YzLMsAp.gif"  width="250">

#### Summary

웹 어플리케이션 버전의 Project Arche는 아키에이지라는 MMORPG에 관한 통계 자료를 제공하는 서비스입니다. backend는 Javascript와 유사한 문법을 사용하는 [Google Apps Script](https://developers.google.com/apps-script/)로 개발하였고, [Google App Engine](https://cloud.google.com/appengine/)에서 호스팅됩니다. [Google Spreadsheets](https://www.google.com/sheets/about/)를 Database처럼 사용합니다. frontend는 [Polymer](https://www.polymer-project.org/)를 사용하여 개발했습니다.

#### Details

통계를 내기 위해 정기적으로 Google Apps Script에서 웹 크롤링 및 파싱을 수행합니다. 정제된 데이터는 Google Spreadsheets에 축적합니다. frontend는 [Google Charts](https://developers.google.com/chart/) 라이브러리를 통해 해당 Spreadsheets의 데이터를 사용자들에게 보여줍니다.

#### Story

개발을 시작할 당시 아키에이지는 꽤 인기 있는 게임이었습니다. 세력 간 대립이 주요 컨텐츠였기 때문에 어떤 세력이 더 강한지, 어떤 세력이 성장하고 있는지가 플레이어들에게 중요한 이슈였습니다. 게임사에서 공식적으로 통계를 내주진 않았으나 각 길드의 정보는 홈페이지에서 제공되었으므로 사용자가 임의로 통계를 내는 것은 가능했습니다.

통계를 내려면 프로그램이 항상 돌고 있어야 하는데, 제 컴퓨터는 24시간 켜 둘 수 없었기 때문에 Google Apps Script라는 클라우드 서비스를 사용하여 웹 파싱을 통해 데이터를 수집하고, 수집된 데이터는 Google Spreadsheets에 저장하게 했습니다. 

#### Usage

이 어플리케이션은 지금은 서비스되고 있지 않습니다. 대신 [동영상](https://www.youtube.com/watch?v=k35ciJNoqR0)으로 체험하실 수 있습니다.

### REST API Server 버전 (2017~)

#### Summary

REST API Server 버전의 Project Arche는 아키에이지 공식 홈페이지에서 제공하는 정보들을 [JSON 형태](https://project-arche.appspot.com/api/auctions/KYPROSA/%EB%AA%A9%EC%9E%AC)로 파싱해주는 서비스입니다. 또한 [Discord](https://discordapp.com/)와 [Webhook](https://en.wikipedia.org/wiki/Webhook)으로 연동한 [아키에이지 알림 서비스](https://goo.gl/forms/AovCs0Au1C0TfcDB3)도 제공하고 있습니다. [Golang](https://golang.org/)으로 개발되어 현재 [Google App Engine](https://cloud.google.com/appengine/)에서 서비스되고 있습니다. Database로 [Google Cloud Datastore](https://cloud.google.com/datastore/)를 사용합니다.

#### Details

주로 HTML로 가져온 데이터를 JSON으로 파싱하는 작업으로 이루어져 있으며, 해당 부분은 [archeage-go](https://github.com/geeksbaek/archeage-go)라는 별도의 패키지로 분리하였습니다.

#### Story

#### Usage

※ REST API 서버 소스는 OAuth 2.0에 사용되는 클라이언트 ID, 비밀키 등이 포함되어 공개하지 않습니다.

### [archeage-go](https://github.com/geeksbaek/archeage-go) (2017~)

archeage-go는 REST API Server 버전의 Project Arche에서 사용되는 핵심적인 기능들을 별도로 분리한 Golang 패키지입니다. HTML 파싱을 지원하는 [goquery](https://github.com/PuerkitoBio/goquery) 라이브러리를 사용합니다.

### [archeage-discord-bot](https://github.com/geeksbaek/archeage-discord-bot) (2017)

archeage-discord-bot은 [archeage-go](https://github.com/geeksbaek/archeage-go) 패키지와 [discordgo](https://github.com/bwmarrin/discordgo)라는 써드파티 API 패키지를 사용해 만든 Discord bot입니다. [Discord](https://discordapp.com/)에 연결해서 사용할 수 있습니다.

***

## [Joongbu Web App](https://github.com/joongbu-capstone-2016-team-01) (2016~2017)

Joongbu Web App은 학교에서 프로젝트 겸 졸업작품으로 개발한 웹 앱입니다.

자세한 설명은 별도의 [문서](https://1drv.ms/w/s!AqKUZ6w7Dq91tHxH3yUTfBusRGWY)에서 확인하실 수 있고, 웹 앱은 [**여기**](https://joongbu-web-app.firebaseapp.com)에서 구경하실 수 있습니다.

***

## [goinside](https://github.com/geeksbaek/goinside) (2016~)

goinside는 디시인사이드라는 웹사이트에서의 행동을 구현한 Go 패키지입니다.

사실 이 패키지는 아래에서 설명해 드릴 [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner)라는 프로그램을 만들면서 프로그램이 점점 커지자 아예 API 패키지를 따로 만드는 게 낫겠다 싶어 작성한 패키지입니다. 대부분의 행동을 구현했으며 [godoc](https://godoc.org/github.com/geeksbaek/goinside)에 자세하게 설명되어 있습니다.

처음에는 실제 디시인사이드 웹사이트의 요청 방식을 모방하여 API를 구현했습니다. 이 방식은 웹사이트 구조가 바뀌면 그때마다 다시 웹사이트를 다시 분석하여 코드를 수정해야 하는 문제가 있습니다. 웹사이트 구조가 바뀌는 일은 비일비재하므로 그다지 좋은 방법은 아니었습니다.

이후에 디시인사이드 어플리케이션에서 별도의 디시인사이드 [내부 REST API](https://github.com/geeksbaek/goinside/blob/master/request.go#L58) 서버와 통신하는 것을 발견했고, 패킷 분석 및 어플리케이션 디컴파일을 통해 내부 API를 분석하여 goinside도 디시인사이드 내부 API를 사용하도록 코드를 수정했습니다. 코드를 개선하면서 효율이 상당히 개선되어 이 패키지로 개발한 프로그램들의 전반적인 퍼포먼스가 향상되었습니다.

### [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler) (2016)

goinside-image-crawler는 디시인사이드에 게시되는 글에서 이미지를 수집하는 프로그램입니다. goinside로 개발한 첫 번째 프로그램이며, 요청에 의해 개발하여 무료로 배포한 프로그램입니다.

Go의 동시성을 활용하여 빠른 속도로 여러 개의 이미지를 다운로드 하는 것이 특징입니다. 중복된 이미지는 건너뛰는 기능이 있습니다.

### [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner) (2016)

<img src="http://i.imgur.com/BnMQy0V.gif" width="700">

goinside-gallog-cleaner는 일명 디시 클리너라고 불리는 프로그램입니다. goinside로 개발한 두 번째 프로그램으로, 디시인사이드에 회원으로 작성한 모든 글과 댓글을 삭제해줍니다.

디시인사이드에는 자신의 글을 일괄 삭제하는 기능이 없었기 때문에 오랜 기간 작성한 글을 하나씩 지우기 힘들어서 이런 작업을 대신 해주는 프로그램이 필요합니다. 오래전에는 무료로 배포되는 프로그램이 있었으나, 최근에는 정상적으로 동작하는 프로그램을 거의 찾을 수 없어 직접 만들게 되었습니다.

무료로 배포 중이며, 이 글을 작성하는 현재 누적 다운로드 수가 1만 4천 번을 넘는, 제 프로그램 중 가장 인기 있는 프로그램입니다.