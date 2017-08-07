<!-- TOC -->
## Table of Contents

- [ourChess (2012)](https://github.com/geeksbaek/portfolio#ourchess-2012)
- [UnlimitedImageCombiner (2012)](https://github.com/geeksbaek/portfolio#unlimitedimagecombiner-2012)
- [Project Arche (2014~)](https://github.com/geeksbaek/portfolio#project-arche-2014)
    - [archeage-go (2017~)](https://github.com/geeksbaek/portfolio#archeage-go-2017)
    - [archeage-discord-bot (2017~)](https://github.com/geeksbaek/portfolio#archeage-discord-bot-2017)
- [go-arp-spoofer (2016)](https://github.com/geeksbaek/portfolio#go-arp-spoofer-2016)
- [Joongbu Web App (2016~2017)](https://github.com/geeksbaek/portfolio#joongbu-web-app-20162017)
- [goinside (2016~)](https://github.com/geeksbaek/portfolio#goinside-2016)
    - [goinside-image-crawler (2016)](https://github.com/geeksbaek/portfolio#goinside-image-crawler-2016)
    - [goinside-gallog-cleaner (2016)](https://github.com/geeksbaek/portfolio#goinside-gallog-cleaner-2016)
- [Deprecated Projects](https://github.com/geeksbaek/portfolio#deprecated-projects)

<!-- /TOC -->

***

## [ourChess](https://github.com/geeksbaek/ourChess) (2012)

<img src="http://i.imgur.com/zqpfsa5.gif" width="400">

ourChess는 웹 기반으로 개발된 1:1 체스게임입니다. backend는 [node.js](https://nodejs.org/), frontend는 Javascript와 약간의 [jQuery](https://jquery.com/)를 사용하여 개발했으며, 그래픽은 HTML5 Canvas API로 2D 이미지를 그려 구현하였습니다. UI는 [bootstrap](http://getbootstrap.com/)을 사용하여 구성하였으며, 사용자들은 [socket.io](https://socket.io/)의 websocket으로 서로 실시간으로 통신합니다. 현재 [heroku](https://www.heroku.com/)에서 무료 할당량을 받아 서비스 중입니다.

이 체스게임의 주요 특징은 플레이어가 기물을 움직이는 모습을 다른 플레이어들이 실시간으로 볼 수 있다는 것입니다. 이를 자연스럽게 구현하기 위해 크게 두 가지 테크닉을 사용했습니다.

- 첫째, 체스판 위에서 기물을 드래그하는 동안 마우스 좌표를 실시간으로 websocket을 통해 브로드캐스트합니다. 구체적으로는 초당 최대 60번까지 브로드캐스트합니다. 드래그 중에 발생하는 mousemove 이벤트는 초당 60번을 초과하여 발생할 수 있으므로, mousemove 이벤트 리스너를 사용하는 대신 setInterval 함수를 동적으로 생성하고 파괴하는 방법을 사용합니다.
- 둘째, 좌표를 브로드캐스트 받은 클라이언트들은 기물이 움직이는 것을 구현하기 위해 Canvas를 다시 그려야 합니다. 이때, 체스 보드가 그려져 있는 메인 Canvas를 다시 그리는 대신 별도의 Canvas를 생성하여 이곳에 움직일 기물을 그린 뒤, CSS Position을 변경하여 움직이도록 합니다. Canvas를 초당 60번씩이나 다시 그리는 것은 비효율적일뿐더러 그래픽 또한 부자연스럽게 보이기 때문에 이 트릭을 사용하였습니다.

개발에서 시간이 가장 많이 들어간 부분은 기물의 움직임이 체스의 규칙을 위반하는지 검사하는 [부분](https://github.com/geeksbaek/ourChess/blob/heroku/public/js/checkAvailability.js)이었습니다. [Stalemate](https://en.wikipedia.org/wiki/Stalemate), [Threefold repetition](https://en.wikipedia.org/wiki/Threefold_repetition), [Promotion](https://en.wikipedia.org/wiki/Promotion_(chess)) 등 대부분의 체스 규칙을 검사하며, 규칙에 위반되는 움직임은 허용되지 않도록 하였습니다.

[여기](https://ourchess.herokuapp.com/)에서 플레이해보실 수 있습니다. 방을 생성하면 고유 URL을 할당받는데, 이 URL을 공유하여 다른 사용자가 입장하면 자동으로 게임이 시작됩니다. 방을 생성한 사람이 White를 잡고, 다음으로 입장한 사람이 Black을 잡습니다. 이후에 입장한 사람들은 관전자가 됩니다. 체스 보드 옆에는 게임 메시지 수신 및 채팅을 할 수 있는 공간이 있습니다.

***

## [UnlimitedImageCombiner](https://github.com/geeksbaek/UnlimitedImageCombiner) (2012)

<img src="http://i.imgur.com/qUFxxam.gif" width="400">

UnlimitedImageCombiner는 웹 브라우저에서 여러 개의 이미지를 하나의 이미지로 합쳐주는 도구입니다. 서버 로직없이 정적 페이지로만 구성된 간단한 어플리케이션입니다. [bootstrap](http://getbootstrap.com/)으로 UI를 구성했으며, HTML5 Canvas API로 이미지를 그려 합치며, Drag and Drop API를 통해 이미지를 드래그하여 순서를 바꿀 수 있습니다.

서버를 통하지 않고 클라이언트 측 기술만을 사용하여 이미지를 합치기 때문에 속도가 빠르며 프라이버시 침해 우려가 없습니다. 또한, 합칠 수 있는 이미지 개수에 제한이 없습니다. 다만 브라우저마다 지원하는 Canvas의 [크기 제한](https://stackoverflow.com/a/11585939)이 있는데, 이 크기를 초과하는 경우에는 두 개 이상의 Canvas로 분리하여 합치도록 하였습니다.

GitHub Pages에서 서비스 중이며 [여기](https://geeksbaek.github.io/UnlimitedImageCombiner/)에서 사용해 보실 수 있습니다.

***

## [Project Arche](https://github.com/geeksbaek/Project-Arche) (2014~)

`#web` `#google_apps_script` `#rest_api` `#google_app_engine` `#polymer` `#webhook`

Project Arche는 아키에이지라는 MMORPG에 대한 프로젝트입니다. 2014년부터 개발되어 지금까지 계속 부수고 만들면서 관리되고 있습니다. 처음에는 게임의 데이터를 주기적으로 수집하여 통계를 내어 보여주는 웹사이트로 시작했다가, 지금은 통계를 내는 대신 경매장 검색, 캐릭터 검색 같은 기능을 제공하는 REST API 서버의 역할을 하고 있습니다.

개발을 시작할 당시 아키에이지는 꽤 인기 있는 게임이었습니다. 세력 간 대립이 주요 컨텐츠였기 때문에 어떤 세력이 더 강한지, 어떤 세력이 성장하고 있는지가 플레이어들에게 중요한 이슈였습니다. 게임사에서 공식적으로 통계를 내주진 않았으나 각 길드의 정보는 홈페이지에서 제공되었으므로 사용자가 임의로 통계를 내는 것은 가능했습니다.

데이터를 내려면 프로그램이 항상 돌고 있어야 하는데, 제 컴퓨터는 24시간 켜 둘 수 없었기 때문에 처음에는 Google Apps Script라는 클라우드 서비스를 사용하여 웹 파싱을 통해 데이터를 수집했습니다. 수집된 데이터는 Google Spreadsheets에 저장하여 통계를 냈습니다. 다른 클라우드 데이터베이스 서비스도 많았지만, 그 당시 가장 빠른 방법을 택했습니다.

클라이언트는 Polymer라는 웹 툴킷을 이용해 개발했습니다. 글을 쓰고 있는 현재는 2.0 버전까지 와있는 Polymer지만, 당시는 0.x버전으로 프로덕션에 사용하기에는 적합하지 않았습니다. 그래도 최신 기술에 관심이 많았던 터라 굳이 사용해보았는데 결과적으로 나쁘지 않았습니다. 통계 사이트는 현재 서비스되고 있지 않지만 [동영상](https://www.youtube.com/watch?v=k35ciJNoqR0)으로 남아있습니다.

게임을 접으면서 서비스를 중단했다가, 2017년 1월에 게임을 다시 시작하면서 프로젝트를 다시 시작하게 되었습니다. 새로운 게임 컨텐츠에 맞춰 웹 앱에 기능을 추가할까 했었는데, 게임이 예전만큼 인기가 없어서 사용하는 사람이 많지 않을 것 같아 포기했습니다.

대신 게임 내 복잡한 아이템의 제작 비용을 계산해주는 시트를 만들어보기로 했습니다. 아이템을 만드는데 필요한 재료 아이템의 가격은 유동적이기 때문에 매번 재료 아이템의 가격을 경매장에서 구해와야 합니다. 이를 위한 [API 패키지](https://github.com/geeksbaek/archeage-go)를 만들었고, Project Arche라는 이름으로 Google App Engine에서 REST API 서버로 서비스하고 있습니다. 계산 시트와 API 서버를 [공개](http://www.inven.co.kr/board/powerbbs.php?come_idx=2641&my=post&l=12554)한 뒤로 많은 사람이 이용하고 있습니다.

지금은 discord의 webhook와 연동하여 공지사항 알리미 같은 서비스를 구현하고 있습니다.

※ github에 남아있는 코드는 웹 앱 개발 중 취소된 버전의 코드이며, REST API로 구현된 현재 서버의 코드는 OAuth 2.0에 사용되는 클라이언트 ID, 비밀키 등이 포함돼있어 공개하고 있지 않습니다.

### [archeage-go](https://github.com/geeksbaek/archeage-go) (2017~)

`#api`

archeage-go는 Project Arche에서 사용되는 핵심 기능을 별도로 분리한 Go 패키지입니다. 아키에이지 공식 홈페이지에서 얻을 수 있는 모든 정보를 API로 구현하려고 했으나 게임을 접으면서 미뤄둔 상태이며 현재 경매장 검색, 캐릭터 검색, 공지사항 가져오기, 서버 상태 조회하기 등의 기능을 지원합니다.

### [archeage-discord-bot](https://github.com/geeksbaek/archeage-discord-bot) (2017)

`#discord` `#bot`

archeage-discord-bot은 [archeage-go](https://github.com/geeksbaek/archeage-go) 패키지와 [discordgo](https://github.com/bwmarrin/discordgo)라는 써드파티 API 패키지를 사용해 만든 discord bot입니다. [discord](https://discordapp.com/)라는 채팅 프로그램에 연결해서 사용할 수 있습니다.

[archeage-go](https://github.com/geeksbaek/archeage-go) 패키지의 기능을 discord에서 사용하기 위해 개발했으나, 현재는 아키에이지를 플레이하지 않게 되어 관리를 잠정 중단한 상태입니다.

***

## [go-arp-spoofer](https://github.com/geeksbaek/go-arp-spoofer) (2016)

`#network` `#security` `#hack` `#tool`

go-arp-spoofer는 학교에서 프로젝트 시간에 개발한 프로그램입니다. 로컬 내에 있는 모든 호스트에게 arp 공격을 수행합니다. 후배 한 명을 포함하며 2명이 개발하였습니다. 저는 arp 스푸핑을 구현하였고 후배는 스푸핑한 패킷에서 ID와 패스워드를 파싱하는 코드를 작성하였습니다.

패킷 캡쳐를 위해 보통 C의 libpcap, C++의 libtins와 같은 라이브러리를 사용하는데, 프로젝트에서 사용되는 언어에 제약이 없었고 Go가 손에 더 익숙했으므로 Go의 [GoPacket](https://github.com/google/gopacket)이라는 라이브러리를 사용해서 개발했습니다.

시연을 위해서, 파싱된 ID와 패스워드가 일부 가려진 채로 웹 페이지에 실시간으로 보이는 기능이 있습니다. 다른 arp 스푸핑 프로그램과 조금 다른 점은 동시에 복수의 사용자를 공격할 수 있는 것에 더하여, 동시에 복수의 네트워크 인터페이스를 통한 공격도 지원한다는 것입니다.

***

## [Joongbu Web App](https://github.com/joongbu-capstone-2016-team-01) (2016~2017)

`#web` `#polymer` `#rest_api` `#open_data` `#google_app_engine`

Joongbu Web App은 학교에서 프로젝트 겸 졸업작품으로 개발한 웹 앱입니다.

자세한 설명은 별도의 [문서](https://1drv.ms/w/s!AqKUZ6w7Dq91tHxH3yUTfBusRGWY)에서 확인하실 수 있고, 웹 앱은 [**여기**](https://joongbu-web-app.firebaseapp.com)에서 구경하실 수 있습니다.

***

## [goinside](https://github.com/geeksbaek/goinside) (2016~)

`#web` `#api`

goinside는 디시인사이드라는 웹사이트에서의 행동을 구현한 Go 패키지입니다.

사실 이 패키지는 아래에서 설명해 드릴 [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner)라는 프로그램을 만들면서 프로그램이 점점 커지자 아예 API 패키지를 따로 만드는 게 낫겠다 싶어 작성한 패키지입니다. 대부분의 행동을 구현했으며 [godoc](https://godoc.org/github.com/geeksbaek/goinside)에 자세하게 설명되어 있습니다.

처음에는 실제 디시인사이드 웹사이트의 요청 방식을 모방하여 API를 구현했습니다. 이 방식은 웹사이트 구조가 바뀌면 그때마다 다시 웹사이트를 다시 분석하여 코드를 수정해야 하는 문제가 있습니다. 웹사이트 구조가 바뀌는 일은 비일비재하므로 그다지 좋은 방법은 아니었습니다.

이후에 디시인사이드 어플리케이션에서 별도의 디시인사이드 [내부 REST API](https://github.com/geeksbaek/goinside/blob/master/request.go#L58) 서버와 통신하는 것을 발견했고, 패킷 분석 및 어플리케이션 디컴파일을 통해 내부 API를 분석하여 goinside도 디시인사이드 내부 API를 사용하도록 코드를 수정했습니다. 코드를 개선하면서 효율이 상당히 개선되어 이 패키지로 개발한 프로그램들의 전반적인 퍼포먼스가 향상되었습니다.

### [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler) (2016)

`#bot`

goinside-image-crawler는 디시인사이드에 게시되는 글에서 이미지를 수집하는 프로그램입니다. goinside로 개발한 첫 번째 프로그램이며, 요청에 의해 개발하여 무료로 배포한 프로그램입니다.

Go의 동시성을 활용하여 빠른 속도로 여러 개의 이미지를 다운로드 하는 것이 특징입니다. 중복된 이미지는 건너뛰는 기능이 있습니다.

### [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner) (2016)

`#bot`

<img src="http://i.imgur.com/BnMQy0V.gif" width="700">

goinside-gallog-cleaner는 일명 디시 클리너라고 불리는 프로그램입니다. goinside로 개발한 두 번째 프로그램으로, 디시인사이드에 회원으로 작성한 모든 글과 댓글을 삭제해줍니다.

디시인사이드에는 자신의 글을 일괄 삭제하는 기능이 없었기 때문에 오랜 기간 작성한 글을 하나씩 지우기 힘들어서 이런 작업을 대신 해주는 프로그램이 필요합니다. 오래전에는 무료로 배포되는 프로그램이 있었으나, 최근에는 정상적으로 동작하는 프로그램을 거의 찾을 수 없어 직접 만들게 되었습니다.

무료로 배포 중이며, 이 글을 작성하는 현재 누적 다운로드 수가 1만 4천 번을 넘는, 제 프로그램 중 가장 인기 있는 프로그램입니다.

***

## Deprecated Projects

### [drawing-quiz](https://github.com/geeksbaek/drawing-quiz) (2016)

Polymer를 사용하여 웹 기반 그림 퀴즈를 개발하다가 의욕 상실로 포기함.

### [go-decrypt-dot11](https://github.com/geeksbaek/go-decrypt-dot11) (2016)

학교 프로젝트로 802.11 packet을 실시간 복호화하는 프로그램을 개발하던 중 다른 일정에 치여 시간 부족으로 포기함.

### [go-network-monitoring](https://github.com/geeksbaek/go-network-monitoring) (2016)

학교 프로젝트로 실시간 네트워크 트래픽을 측정하는 프로그램을 개발했으나 중규모 이상 트래픽에서는 정상적인 측정이 어려울 정도로 퍼포먼스가 떨어지는 문제가 있음.
