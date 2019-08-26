# Portfolio

이 페이지는 제 개인 프로젝트 중 몇 가지를 추려 소개합니다.

## 기술 스택

개인 프로젝트에서 사용한 기술 스택입니다. 숙련된 기술은 **굵게** 강조했습니다.

- 언어
  - **Go**
  - **JavaScript (ES2015)** / node.js
- 프레임워크 / 툴킷
  - React
  - Polymer
  - **Dialogflow**
- 퍼블릭 클라우드
  - **Firebase**
  - **Google Cloud Platform**

***

## Table of Contents

- [pokedex (2018~)](https://github.com/geeksbaek/portfolio#pokedex-2018)
- [goinside (2016~2018)](https://github.com/geeksbaek/portfolio#goinside-20162018)
- [ourchess (2012)](https://github.com/geeksbaek/portfolio#ourchess-2012)
- [etc.](https://github.com/geeksbaek/portfolio#etc)

## [pokedex](https://github.com/geeksbaek/pokedex) (2018~)

[![GitHub stars](https://img.shields.io/github/stars/geeksbaek/pokedex.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/geeksbaek/pokedex/stargazers/)

`#go` `#javascript` `#web_scraping` `#firebase` `#dialogflow` `#google_assistant` `#chatbot`

### 요약

pokedex는 Pokémon GO 라는 모바일 게임의 플레이를 보조하기 위한 일종의 챗봇입니다. 음성 또는 텍스트로 대화를 할 수 있습니다. 예를 들어 휴대전화에 대고 `Ok, Google. 리자몽 약점 뭐야?` 라는 질문을 할 수 있습니다.

(pokedex는 Actions on Google(AoG) 이라고 부르는 Google Assistant 플랫폼에서 동작합니다. [Dialogflow](https://cloud.google.com/dialogflow/) 기반으로 개발되었으며 이에 대한 자세한 설명은 [여기](https://github.com/dialogflow/resources)에 소개되어 있습니다)

### 자세히

pokedex는 프론트엔드 격인 Dialogflow Agent와 백엔드 격인 Fulfillment 서버, 그리고 포켓몬 DB로 구성되어 있으며 아래와 같은 방식으로 동작합니다.

<p align="center">
  <img src="https://raw.githubusercontent.com/dialogflow/resources/master/images/overview.png" width="1000">
</p>

1. 사용자의 요청이 AoG를 통해 Agent로 전달되면 Agent는 의도를 파악하고 파싱을 시도합니다.
2. 의도가 파악되면 파싱 결과를 Fulfillment라는 WebHook 서버로 보냅니다.
3. Fulfillment는 파싱된 요청을 받아 적절한 응답을 생성해 돌려줍니다.

예를 들어 `리자몽 약점 뭐야?`라는 요청을 받게 되었을 때, Agent는 미리 정의한 의도 중에서 `약점`과 관련된 의도가 존재하는 것을 확인하고, 해당 의도에서 전달받을 수 있는 인자인 키워드 `리자몽`을 파싱합니다. Fulfillment로 `약점`이라는 의도와 `리자몽`이라는 인자가 전달되면 Fulfillment는 DB를 참조해서 적절한 응답을 생성하여 반환하게 됩니다.

DB는 [gameinfo.io](https://pokemon.gameinfo.io/ko/)라는 웹사이트를 스크래핑하여 구축했습니다. 게임 특성상 포켓몬 데이터는 수정될 일이 거의 없기 때문에 DB 서버를 두는 대신에 데이터를 JSON 파일로 직렬화하여 Fulfillment 서버와 함께 두고 전역 변수에 JavaScript 객체로 불러와 접근하도록 했습니다.

### 비하인드 스토리

포켓몬 GO의 레이드 컨텐츠에서 사용하려는 목적으로 개발했습니다. 포켓몬의 상성을 따져보고 유리한 덱을 구성해야 하는데 검색을 하지 않는 이상 한계가 있기 때문입니다. 브라우저를 키고 상성을 검색하는 시간을 더 단축시키고 싶었습니다. pokedex를 이용하면 말 한마디로 상성을 확인할 수 있습니다. 상성 뿐 아니라 IV 차트 보기, 포켓몬 둥지 찾기 등 다양한 기능을 추가 개발하고 있습니다.

대부분의 개인 프로젝트가 그러하듯이 pokedex도 개인적인 필요에 의해 개발된 프로젝트이지만, 이번에는 GCP 크레딧을 얻기 위한 목적도 있었습니다. Google Assistant 개발자들에게 1년간 매월 200달러의 크레딧을 주는 [프로그램](https://developers.google.com/actions/community/overview)이 있는데, pokedex 덕분에 프로그램에 통과되어 이후 다른 프로젝트에서 GCP 리소스를 마음 편히 사용할 수 있게 되었습니다.

### 사용해보기

휴대전화에서 구글 어시스턴트를 호출한 뒤 `포켓몬 도감과 대화`와 같은 명령으로 pokedex를 호출하거나 [여기](https://assistant.google.com/services/a/uid/000000ff71813a93?hl=ko)에서 pokedex를 실행하는 명령을 휴대전화로 보낼 수 있습니다. (Android 5.0 이상의 휴대전화, iOS 10.0 이상의 기기에서 사용할 수 있습니다)

<p align="center">
  <img src="https://raw.githubusercontent.com/geeksbaek/portfolio/master/src/default.gif" width="250">
</p>

## [goinside](https://github.com/geeksbaek/goinside) (2016~2018)

[![GitHub stars](https://img.shields.io/github/stars/geeksbaek/goinside.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/geeksbaek/goinside/stargazers/)

`#go` `#web_scraping` `#lib`

### 요약

goinside는 디시인사이드라는 포털에서의 행동을 Go로 구현한 라이브러리입니다. 초기에는 웹 페이지를 스크래핑하는 방식으로 기능을 구현했으나 디시인사이드 안드로이드 앱에서 사용하는 비공개 API를 발견하여 현재는 디시인사이드 API의 래퍼 형태로 구현되어 있습니다.

goinside는 제가 개발한 라이브러리 중에서 가장 큰 라이브러리입니다. 최대한 많은 기능을 지원하기 위해 노력했고, 디시인사이드 API에서 지원하지 않는 갤로그 관련 기능도 웹 스크래핑으로 일부 구현했습니다. Go 언어를 최대한 이용하여 간결하고 유연하게 설계했으며 함수 대부분을 커버하는 테스트 코드를 작성하여 유지 보수에 신경 썼습니다.

### 자세히

디시인사이드 비공개 API를 래핑하기 위해서 우선 해당 API의 사용 방법을 정확히 익혀야 했습니다. 이 API에 대한 문서 같은 것은 존재하지 않았기 때문에, 서버와 앱이 통신하는 패킷을 분석하고 앱 자체를 디컴파일해서 분석하는 방법을 사용했습니다. 앱은 난독화 되어있었기 때문에 분석이 쉽지는 않았습니다.

그 외에 기본적인 기능들을 래핑하는 것은 어렵지 않았는데, 다만 갤로그에 대해서는 API가 존재하지 않았기 때문에 [goinside/gallog](https://godoc.org/github.com/geeksbaek/goinside/gallog) 라는 이름의 서브 패키지에서 웹 스크래핑을 통해 기능을 구현했습니다. goinside/gallog 에는 [Session.FetchAll](https://godoc.org/github.com/geeksbaek/goinside/gallog#Session.FetchAll), [Session.DeleteAll](https://godoc.org/github.com/geeksbaek/goinside/gallog#Session.DeleteAll)과 같은 Batch 작업을 수행하는 함수가 있는데, Go가 동시성을 잘 지원하는 덕분에 쉽게 구현할 수 있었습니다.

현재 테스트 코드의 커버리지는 약 80%이며 지속해서 코드의 안정성을 개선하고 있습니다. (travis 빌드 도구를 통해 측정된 커버리지는 로컬에서만 수행할 수 있는 일부 테스트 코드를 주석처리 했기 때문에 정확하지 않습니다)

### 비하인드 스토리

사실 이 라이브러리는 하위 프로젝트 [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner)라는 프로그램을 개발하는 중에 점점 커지는 코드를 더 잘 관리하기 위해 분리한 것입니다. API 라이브러리를 만들어 오픈소스로 공개하면 수요가 있을 것이라고 생각했습니다.

처음에는 실제 디시인사이드 웹사이트를 스크래핑하여 API를 구현했습니다. 이 방식은 웹사이트 구조가 바뀌면 그때마다 다시 웹사이트를 다시 분석하여 코드를 수정해야 하는 문제가 있습니다. 웹사이트 구조가 바뀌는 일은 비일비재하므로 그다지 좋은 방법은 아니었습니다. 이후에 디시인사이드 어플리케이션에서 비공개 API 서버와 통신하는 것을 발견했고, 대대적으로 코드를 개선하면서 성능 및 유지보수 비용이 크게 개선되었습니다.

### 하위 프로젝트

#### [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler)

[![GitHub stars](https://img.shields.io/github/stars/geeksbaek/goinside-image-crawler.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/geeksbaek/goinside-image-crawler/stargazers/) [![Github All Releases](https://img.shields.io/github/downloads/geeksbaek/goinside-image-crawler/total.svg)]()

`#vision`

goinside-image-crawler는 게시물의 이미지를 수집하는 프로그램입니다. 여러 개의 이미지를 동시적으로 내려받으며 [Google Cloud Vision API](https://cloud.google.com/vision/)와 연동하여 수집한 이미지를 분류하는 기능이 있습니다.

#### [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner)

[![GitHub stars](https://img.shields.io/github/stars/geeksbaek/goinside-gallog-cleaner.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/geeksbaek/goinside-gallog-cleaner/stargazers/) [![Github All Releases](https://img.shields.io/github/downloads/geeksbaek/goinside-gallog-cleaner/total.svg)](https://github.com/geeksbaek/goinside-gallog-cleaner/releases/latest)

goinside-gallog-cleaner는 일명 디시 클리너라고 불리는 프로그램입니다. 회원으로 작성한 모든 글과 댓글을 삭제해줍니다.

디시인사이드에는 자신의 글을 일괄 삭제하는 기능이 없기 때문에 이런 작업을 대신 해주는 프로그램에 대한 수요가 항상 있었습니다. 현재는 사용할 수 없지만 누적 다운로드가 수 만 건을 기록했을 정도로 인기 있던 프로그램입니다.

***

## [ourchess](https://github.com/geeksbaek/ourchess) (2012)

[![GitHub stars](https://img.shields.io/github/stars/geeksbaek/ourchess.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/geeksbaek/ourchess/stargazers/)

`#javascript` `#nodejs` `#websocket` `#gcp`

### 요약

ourchess는 웹 기반으로 개발된 멀티플레이어 1:1 체스게임입니다. Backend는 node.js, Frontend는 JavaScript와 약간의 jQuery를 사용하여 개발했으며, HTML5 Canvas API로 2D 이미지를 그려 그래픽을 구현하였습니다. UI는 Bootstrap을 사용하여 구성하였으며, 사용자들은 Socket.io의 websocket으로 서로 실시간으로 통신합니다. 현재 [Google Cloud Run](https://ourchess-fyinkdszda-uc.a.run.app/)에서 서비스 중입니다.

### 자세히

멀티플레이어 게임이므로, 사용자들은 각자 방을 생성하여 동시에 게임을 플레이할 수 있습니다. socket.io가 서버에 연결된 소켓들을 네임스페이스로 구분하는 기능을 지원하는 덕분에 방을 쉽게 구현할 수 있었습니다. 방을 생성하면 랜덤한 문자열이 생성되는데, 이 문자열을 네임스페이스로 사용하여 방을 구분 짓습니다.

<p align="center">
  <img src="http://i.imgur.com/XhWvXj2.png" width="170"> <img src="http://i.imgur.com/M5uApvG.png" width="170">
</p>

멀티스크린 지원도 해상도가 변경되면 화면 방향을 계산한 뒤 UI를 재배치하여 모바일 환경에서도 자연스럽게 보이도록 하였습니다. 당시에는 CSS 미디어 쿼리같은 기능이 없었기 때문에 jQuery 기반으로 구현했던 것으로 기억합니다.

이 체스 게임의 주요 특징은 플레이어가 기물을 움직이는 모습이 다른 플레이어에게 실시간으로 전달된다는 것입니다. 이를 자연스럽게 구현하기 위해 크게 두 가지 테크닉을 사용했습니다.

1. 체스판 위에서 기물을 드래그하는 동안 마우스 좌표를 실시간으로 websocket을 통해 브로드캐스트합니다. 현재 코드에서는 mousemove 이벤트가 발생했을 때 좌표 브로드캐스트 하게 되어있는데, 지금 생각해보니 mousemove 이벤트 대신 mousedown, mouseup 같은 이벤트의 리스너에 브로드캐스트를 수행하는 setInterval 함수를 동적으로 생성 및 파괴하는 코드를 구현하는 것이 더 나아 보입니다. mousemove 이벤트는 초당 60회 이상 발생할 수 있는데 그렇게 자주 브로드캐스트 하는 것은 낭비라고 생각됩니다)

2. 좌표를 브로드캐스트 받은 클라이언트들은 기물이 움직이는 것을 구현하기 위해 Canvas를 다시 그려야 합니다. 이때 체스 보드가 그려져 있는 메인 Canvas를 다시 그리는 대신 별도의 Canvas를 생성하여 이곳에 움직일 기물을 그린 뒤 CSS Position을 변경하여 움직이도록 했습니다. Canvas를 초당 60회 이상 다시 그리는 것은 비효율적일뿐더러 그래픽 또한 부자연스럽게 보이기 때문에 이 트릭을 사용하였습니다.

<p align="center">
  <img src="http://i.imgur.com/zqpfsa5.gif" width="400">
</p>

### 비하인드 스토리

온라인 멀티플레이어 체스 게임을 만들기로 한 뒤 제가 가장 중요하게 생각한 목표는 "비록 컴퓨터를 사이에 놓고 두는 체스지만 진짜 사람을 마주보고 있다는 기분을 들게 하자" 였습니다. 어떻게 해야 그런 기분을 들게 할 수 있을지 고민한 끝에 상대가 움직이고 있는 기물의 움직임을 실시간으로 보여주기로 했습니다. 이 아이디어를 실현하기 위해 많은 시행착오를 거치면서 기술을 개선한 끝에 만족스러운 결과를 얻게 되었습니다.

개발에서 시간이 가장 많이 들어간 부분은 기물의 움직임이 체스의 규칙을 위반하는지 검사하는 코드를 작성하는 부분이었습니다. Stalemate, Threefold repetition, Promotion 등 대부분의 체스 규칙을 검사하며, 규칙에 위반되는 움직임은 허용되지 않도록 하였습니다. 사실 이 부분은 서버에서 검사해야 하지만, 개발 편의상 클라이언트에서 검사하게 했습니다. 제대로 서비스하려면 이러한 부분은 보완을 거쳐야 합니다.

이 어플리케이션은 제가 처음으로 개발한 프로그램이어서 의미가 남다릅니다. 대학교 1학년을 마친 뒤 군 휴학 중에 한 달 동안 집에 틀어박혀서 개발했는데, 질문하거나 조언을 구할 사람이 없었기 때문에 모든 것을 혼자서 찾아 배워야 했습니다. 이 과정에서 스스로 문제를 해결하는 능력을 기르고, 혼자서도 하나의 프로젝트를 완성할 수 있다는 자신감을 얻었습니다.

### 사용해보기

[이곳](https://ourchess-fyinkdszda-uc.a.run.app/)에서 직접 플레이해보실 수 있습니다. 플랫폼으로 사용 중인 Google Could Run이 아직 WebSocket을 완전히 지원하지 않아 모든 기능이 동작하지는 않습니다.

## Etc

### [Tesla Model 3 Earlybird](https://github.com/geeksbaek/tesla-model-3-earlybird)

`#react` `#firebase`

테슬라 모델 3의 한국 출시를 기다리며 개발한 서비스입니다. 최신 환율 정보를 바탕으로 예상 구매 가격을 계산해줍니다. 최근 모델 3가 정식 오픈하게 되면서 지원을 중지하게 되었습니다. [여기](https://geeksbaek.github.io/tesla-model-3-earlybird/#/)에서 호스팅은 유지되고 있습니다.

### [Project Arche](https://github.com/geeksbaek/Project-Arche)

`#go` `#web_scraping` `#gcp` `#polymer` `#restful`

아키에이지라는 MMORPG 사용자들에게 도움을 주기 위해 개발한 서비스입니다. 지금은 서비스가 중지된 웹 어플리케이션 버전과 현재 서비스되고 있는 API 버전으로 나누어져 있습니다. [여기](https://project-arche.appspot.com/api/auctions/total/%EB%AA%A9%EC%9E%AC/10)에서 API 버전을 테스트할 수 있습니다.

<p align="center">
  <img src="http://i.imgur.com/hvVFxEz.gif" width="300"> <img src="http://i.imgur.com/YzLMsAp.gif"  width="300">
</p>

### [go-arp-spoofer](https://github.com/geeksbaek/go-arp-spoofer)

`#go` `#network`

대학교에서 "ARP Spoofing을 통한 ID, PASSWORD 파싱" 이라는 주제로 개발한 ARP 스푸핑 툴입니다. Go의 동시성 특징을 적극적으로 활용하여 개발되었습니다. 동시에 복수의 인터페이스, 복수의 세션을 동시에 공격할 수 있는 특징이 있습니다. 자세한 설명은 [PPT](https://onedrive.live.com/redir?resid=75AF0E3BAC6794A2!5977&authkey=!AMk1emIWlg96vk8&ithint=file%2cpptx)에 소개되어 있습니다.

### [go-network-monitoring](https://github.com/geeksbaek/go-network-monitoring)

`#go` `#network`

대학교에서 개발한 네트워크 트래픽 통계 툴입니다. 마찬가지로 Go로 개발하였으며, 네트워크 in-path 구간에서 사용할 수 있습니다. 최적화를 고려하지 않고 간단하게 만들었기 때문에 일정 트래픽 이상이 발생하는 네트워크에서는 정상적인 통계를 내지 못할 수 있습니다.

<p align="center">
  <img src="http://i.imgur.com/FkjatPv.png">
</p>
