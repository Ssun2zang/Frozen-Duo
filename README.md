# Frozen Duo 게임 소개

Frozen Duo는 두 플레이어(펭귄과 북극곰)가 함께 퍼즐을 풀며 꽃을 찾아가는 퍼즐 어드벤처 게임입니다. 플레이어는 각자의 캐릭터를 조작하며, 화면 분할 로컬 멀티 게임 모드에서 협력하여 다양한 퍼즐을 해결하고 목적지에 도달해야 합니다.

## 특징

- **장르** : 퍼즐 어드벤처
- **플랫폼** : Windows
- **게임 엔진** : Unity 2022.3.8f1
- **게임 모드** : 화면 분할 로컬 멀티 게임

## 게임 개발

### 캐릭터
- Player1(펭, 펭귄)
- Player2(벤, 북극곰)
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/b26ed70d-4c3d-4556-99d2-8e51db126780)


### 애니메이션
- 펭귄과 북극곰 눈 깜박이기, 펭귄과 북극곰 이동, 펭귄과 북극곰 사다리타기
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/bb94a9ec-82bd-485f-9600-da2e3cf89d73)


### 컨트롤
- Player1 : 이동(w,a,s,d), 시야 회전(left shift key, z key)
- Player1 : 이동(up,down,right,left), 시야 회전(right shift key, slash key(/))
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/a2ae4881-4f0a-437b-b484-3a1d49f0309c)


### 스테이지 구성
- 얼음 섬 : 게임은 얼음 섬에서 시작합니다. 얼음 성에는 간단한 퍼즐이 있습니다. 여러가지 장애물과 퍼즐을
클리어하고 최종 목적지인 배에 함께 도착해야 합니다. 몇개의 퍼즐은 펭귄과 북극곰이 함께 협동
플레이를 해야 합니다. 배에 다다르면 스테이지를 클리어할 수 있습니다.
- 기믹
- 플레이어가 밀 수 있는 빛 반사판을 활용한 얼음 녹이기
- 북극곰이 올라가면 깨지는 얼음과 펭귄이 밀리는 바람을 피해서 퍼즐 넘어가기
- 쫓아오는 눈사람 피하기
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/9a231cbe-e508-451b-b0e3-f2dc2bfb8313)

- 꽃밭 미로 : 얼음성의 다음 스테이지인 꽃밭 미로에서는 미로의 입구에서 시작하게 됩니다. 플레이어는 서로
다른 위치에서 시작하고, 미로와 함께 여러가지 장애물을 피해 꽃 동산에 도착하면 스테이지를
클리어할 수 있습니다. 클리어 후 엔딩 컷신이 재생됩니다.
- 기믹
- 미로에 숨어있는 가시에 찔리면 게임 오버
- 펭귄이 올라와 있는 버섯위로 북극곰이 떨어지면 펭귄이 날아가는 점프버섯
- 두 플레이어가 각각 발판을 밟아 문 넘어뜨리기
- 두 플레이어가 함께 장벽을 밀어서 깨뜨리기
- 커다란 돌을 밀어서 구덩이 막기
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/1ba5e1bf-7a7a-45c4-a051-0f3ba02e353f)

### 게임 규칙
- 퍼즐을 클리어 하면 스테이지 클리어
• 스테이지1: 배 앞에 도착
• 스테이지2: 꽃밭에 도착
- 바다에 빠지면 게임오버
- 눈사람에 부딪히면 게임오버
- 가시에 닿으면 게임오버

### 게임 오브젝트, 스크립트

- **카메라**

플레이어로부터 특정한 거리를 유지하기 위해 Offset을 설정하고, Lerp 방식을 이용하여 현재
위치에 따라 부드럽게 이동합니다.

- **캐릭터**

각 캐릭터 유형에 따라 WASD 또는 화살표 키를 사용하여 이동할 수 있으며, L-shift, ‘z’ / R-shift,
‘/’ 키로 카메라 회전이 가능합니다.

- **눈사람**

플레이어를 따라다니며, 플레이어와 충돌 시, 게임 오버 로직이 실행됩니다.

- **바람**

Player 1(펭귄)이 해당 스크립트의 영향을 받는 특정 구역에 진입하면 정해진 방향으로
AddForce로 가속 시킵니다.

- **깨지는 얼음**

여러 얼음 파편을 Child Object로 가지며, 일반 상태에서는 물리적 영향을 받지 않습니다. Player
2(북극곰)이 충돌하면 해당 얼음의 child object 에 rigid body 를 활성화시켜 중력에 따라
무너지도록 만들어졌습니다.

- **빛 반사판**

Ray cast 를 사용하여 바라보는 방향(z-축)에 녹는 얼음 벽이 있으면 해당 얼음 벽의 Laser
카운트를 1만큼 감소시킵니다.

- **녹는 얼음 벽**

빛 반사판을 통해 Laser 카운트를 감소시키고, 카운트가 0이 되면 얼음이 녹습니다. Custom
shader를 사용하여 얼음 녹는 모습을 표현하며, vertex shader에서 오브젝트 높이에 따라 height
map을 적용합니다.

- **밀 수 있는 블럭**

Player 2(북극곰)과 충돌 시, 충돌 지점의 normal vector를 계산하여 해당 방향의 x축 또는 z축
중 더 큰 방향으로 블럭을 일정 거리만큼 이동시킵니다.

- **점프 버섯**

Player 1(펭귄)이 충돌 중일 때, Player 2(북극곰)이 버섯 위에서 충돌하면 Player 1 을
점프시킵니다. 충돌 방향의 y축 크기가 일정 값(0.5)보다 큰지 확인하여 점프 여부를 결정합니다.

## UI
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/bb1274e5-5aea-4db6-a6ed-47a6626e16b4)
![image](https://github.com/sodaakim/Frozen-Duo/assets/83997634/a132cc7b-7acf-4641-8ed1-fd4c632272b7)


## 실행 방법

1. [Frozen Duo의 GitHub 릴리스 페이지](https://github.com/sodaakim/Frozen-Duo/releases)로 이동합니다.
2. 최신 버전을 확인합니다.
3. 최신 버전의 `Frozen.Duo.zip` 파일을 다운로드하고 압축을 해제합니다.
4. `FROZEN DUO GAME.exe` 파일을 실행합니다.

## 팀원 역할

- **김민기**
- 꽃밭 씬 미로 기획과 제작, 게임 기믹(바람), 미로 장애물 제작

- **김소희**
- 카메라-플레이어 제어, 캐릭터 애니메이션 제작, 콜라이더 제작, 장애물(깨지는 얼음) 제작, ppt

- **박진영**
- 얼음섬 기획과 맵 제작, 게임 기믹 (반사판, 녹는 얼음) 제작, 발표

- **장혜정**
- 카메라-플레이어 제어, 장애물(눈사람, 미는 블록, 점핑 버섯) 제작, 게임 매니저 및 UI 제작

## 지원

게임 실행 중 문제가 발생하거나 피드백이 있는 경우, GitHub 이슈 트래커를 통해 문의할 수 있습니다. 사용자의 의견은 게임 개선에 큰 도움이 됩니다.

