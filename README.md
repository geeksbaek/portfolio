# Portfolio

## [ourChess](https://github.com/geeksbaek/ourChess) (2012~)

#game #web #websocket #html5 #canvas #nodejs #spa

ourChess는 온라인 1:1 체스게임입니다. 대학교 1학년을 마친 뒤 군 휴학 중에 개발했습니다. ourChess는 제가 만든 첫 어플리케이션이기도 합니다. node.js로 구동되는 SPA이며 지금도 heroku에서 무료 할당량을 받아 서비스되고 있습니다.

온라인 멀티플레이어 체스 게임을 만들기로 한 뒤, 제가 가장 중요하게 생각한 목표는 "비록 컴퓨터로 두는 체스지만, 진짜 사람과 두는 기분을 들게 하자" 였습니다. 어떻게 해야 그런 기분을 들게 할 수 있을지 고민한 끝에, 상대가 기물을 들고 움직이는 모습을 실시간으로 보여주면 좋을 것 같았습니다. 이 아이디어를 실현하기 위해 많은 시행착오를 거치고 나서 Canvas API가 가장 적합하다고 판단해 이 기술을 사용하게 되었습니다.

처음에는 마우스 이동 이벤트가 발생할 때마다 모든 사람에게 마우스 좌표를 Websocket으로 브로드캐스팅하여 각각의 클라이언트에서 캔버스를 새로 그리게끔 하여 실시간 움직임을 구현하였습니다. 그러나 이 방법은 크게 비효율적이었습니다. 고민 끝에 하나의 Canvas에서 모든 작업을 하던 방법 대신, 체스 보드를 그리는 Canvas와 움직이는 기물을 그리는 Canvas를 분리하는 것 문제를 해결했습니다. 움직이는 기물을 그리는 Canvas는 좌표가 변경될 때마다 매번 새로 그리는 대신 Canvas의 CSS position을 변경하는 방법으로 자연스러운 움직임을 보여줄 수 있었습니다.

[**여기**](https://ourchess.herokuapp.com/)에서 플레이해보실 수 있습니다. 방을 생성한 사용자가 해당 방의 URL을 공유하여 게임 상대를 초대할 수 있습니다. 방을 생성한 사람이 White를 잡고, 두 번째로 입장한 사람이 Black을 잡습니다. 이후에 입장한 사람들은 자동으로 관전자가 됩니다.

## [UnlimitedImageCombiner](https://github.com/geeksbaek/UnlimitedImageCombiner) (2012~)

#tool #web #html5 #canvas #spa

UnlimitedImageCombiner는 브라우저에서 이미지를 손쉽게 합칠 수 있도록 도와주는 도구입니다. 

예전에는 인터넷에 글을 작성할 때, 첨부할 수 있는 이미지 파일 개수에 제한이 있는 경우가 많았습니다. 그래서 여러 장의 이미지를 하나로 합치는 프로그램을 자주 사용했는데, 개인적으로 불편한 점이 몇 가지 있었습니다. 윈도우용 앱은 설치의 번거로움과 악성 프로그램일지 모른다는 위험이 있었고, [기존 웹 앱](http://bbom.org/tools/)의 경우는 이미지를 서버로 전송하여 합친 뒤 결과물을 다시 돌려주는 방식이었기 때문에 속도도 느리고 인터넷 연결이 필요하다는 단점이 있었습니다.

프로그램을 설치할 필요가 없는 웹 앱의 장점을 살리면서도 사용하기 쉬운 새로운 앱의 만들어보고 싶었습니다. 그래서 브라우저에서 지원하는 웹 기술만으로 이미지를 합치는 도구를 만들게 되었습니다.

클라이언트 측 기술만을 사용하여 이미지를 합치기 때문에 서버가 필요 없습니다. 따라서 매우 빠른 속도로 합칠 수 있습니다. 이미지 개수의 제한도 없앴습니다. 군더더기를 최대한 줄여 수직으로만 합칠 수 있게 했고, 이미지 크기는 최대 폭 기준, 최소 폭 기준, 수동 폭 기준. 이렇게 3가지 중 하나만 선택할 수 있게 했습니다.

서버가 필요 없는 단순한 웹 앱이기 때문에 github pages로 서비스 중입니다. [**여기**](https://geeksbaek.github.io/UnlimitedImageCombiner/)에서 사용해 보실 수 있습니다.

## [Project Arche](https://github.com/geeksbaek/Project-Arche) (2014~)

### [archeage-go](https://github.com/geeksbaek/archeage-go) (2017~)

### [archeage-discord-bot](https://github.com/geeksbaek/archeage-discord-bot) (2017~)

## [go-arp-spoofer](https://github.com/geeksbaek/go-arp-spoofer) (2016~)

## [Joongbu Web App](https://github.com/joongbu-capstone-2016-team-01) (2016~)

## [goinside](https://github.com/geeksbaek/goinside) (2016~)

### [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler) (2016~)

### [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner) (2016~)
