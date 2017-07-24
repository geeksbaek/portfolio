# Portfolio

## [ourChess](https://github.com/geeksbaek/ourChess) (2012~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/ourChess.svg?style=social&label=Star)](https://github.com/geeksbaek/ourChess)

#game #websocket #html5 #canvas #nodejs #spa

ourChess는 온라인 1:1 체스게임입니다. 대학교 1학년을 마친 뒤 군휴학 중에 개발했습니다. ourChess는 제가 만든 첫 어플리케이션이기도 합니다. node.js로 구동되는 SPA입니다. 지금도 heroku에서 무료 할당량을 받아 서비스되고 있습니다.

온라인 멀티플레이어 체스 게임을 만들기로 결정한 뒤, 제가 가장 중요하게 생각한 목표는 "비록 컴퓨터로 두는 체스지만, 진짜 사람과 두는 기분을 들게 하자" 였습니다. 어떻게 해야 그런 기분을 들게 할 수 있을 지 고민한 끝에, 상대가 기물을 들고 움직이는 모습을 실시간으로 보여주면 좋을 것 같았습니다. 이 아이디어를 실현하기 위해 많은 시행 착오를 거치고 나서 Canvas API가 가장 적합하다고 판단해 이 기술을 사용하게 되었습니다.

처음에는 마우스 이동 이벤트가 발생할 때마다 모든 사람들에게 마우스 좌표를 Websocket으로 브로드캐스팅하여 각각의 클라이언트에서 캔버스를 새로 그리게끔 하여 실시간 움직임을 구현하였습니다. 그러나 이 방법은 크게 비효율적이었습니다. 고민 끝에 하나의 Canvas에서 모든 작업을 하던 방법 대신, 체스 보드를 그리는 Canvas와 움직이는 기물을 그리는 Canvas를 분리하는 것 문제를 해결했습니다. 움직이는 기물을 그리는 Canvas는 좌표가 변경될 때마다 매번 새로 그리는 대신 Canvas의 CSS position을 변경하는 방법으로 자연스러운 움직임을 보여줄 수 있었습니다.

[**여기**](https://ourchess.herokuapp.com/)에서 플레이 해보실 수 있습니다. 방을 생성한 유저가 해당 방의 URL를 공유하여 게임 상대를 초대할 수 있습니다. 방을 생성한 사람이 White를 잡고, 두 번째로 입장한 사람이 Black을 잡습니다. 이후에 입장한 사람들은 자동으로 관전자가 됩니다.

## [UnlimitedImageCombiner](https://github.com/geeksbaek/UnlimitedImageCombiner) (2012~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/UnlimitedImageCombiner.svg?style=social&label=Star)](https://github.com/geeksbaek/UnlimitedImageCombiner)

## [Project Arche](https://github.com/geeksbaek/Project-Arche) (2014~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/Project-Arche.svg?style=social&label=Star)](https://github.com/geeksbaek/Project-Arche)

### [archeage-go](https://github.com/geeksbaek/archeage-go) (2017~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/archeage-go.svg?style=social&label=Star)](https://github.com/geeksbaek/archeage-go)

### [archeage-discord-bot](https://github.com/geeksbaek/archeage-discord-bot) (2017~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/archeage-discord-bot.svg?style=social&label=Star)](https://github.com/geeksbaek/archeage-discord-bot)

## [go-arp-spoofer](https://github.com/geeksbaek/go-arp-spoofer) (2016~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/go-arp-spoofer.svg?style=social&label=Star)](https://github.com/geeksbaek/go-arp-spoofer)

## [Joongbu Web App](https://github.com/joongbu-capstone-2016-team-01) (2016~) 

## [goinside](https://github.com/geeksbaek/goinside) (2016~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/goinside.svg?style=social&label=Star)](https://github.com/geeksbaek/goinside)

### [goinside-image-crawler](https://github.com/geeksbaek/goinside-image-crawler) (2016~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/goinside-image-crawler.svg?style=social&label=Star)](https://github.com/geeksbaek/goinside-image-crawler)

### [goinside-gallog-cleaner](https://github.com/geeksbaek/goinside-gallog-cleaner) (2016~) [![GitHub stars](https://img.shields.io/github/stars/geeksbaek/goinside-gallog-cleaner.svg?style=social&label=Star)](https://github.com/geeksbaek/goinside-gallog-cleaner)
