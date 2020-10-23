# word-chain-game
## 끝말잇기 콘솔 게임

### CS 프로그램

- **부분 `stateful` 방식** : 서버와 클라이언트의 통신은 다음과 같은 형식을 갖는다.
  - 클라이언트 & 서버 연결
  - 클라이언트 -> 서버 : 아이디 정보 전송
  - 서버 -> 클라이언트 : 화면 정보 전송
  - 클라이언트 -> 서버 : 요구사항 전송
  - 서버 -> 클라이언트 : 요구 작업 수행 (stateful)
  - 클라이언트 & 서버 연결 종료
- **요구 작업을 수행**하는 동안에는 중간에 <u>**연결이 끊기지 않으며**</u>, 특히 게임 메뉴에서 싱글 게임과 멀티게임을 고르는 화면부터 각 게임을 하는 시점까지 연결이 지속된다. 
- 클라이언트의 **<u>인증 방식</u>** : **사용자가 로그인을 하면** **서버는 클라이언트에게** **회원의 정보인 아이디**(보통은 인증을 위한 암호가 사용되겠지만, 편의를 위해서 아이디로 설정)를 보내주며 클라이언트는 아이디를 내부에 저장하고, 클라이언트가 요청을 시도할 때마다 **이 아이디 정보를 보내어 서버에 회원 인증**을 한다. 로그아웃을 하면 **서버는 클라이언트에게 내부의 저장된 아이디를 삭제 요청**하고, 클라이언트는 저장된 아이디를 삭제하여 다시 **비회원 상태로 서버에 접속**할 수 있게 된다.
- 회원에 따른 **<u>화면 전송 방식</u>** :  **클라이언트 측에서 주는 아이디 정보**를 갖고 인증 과정을 거쳐 그에 따른 화면을 띄운다. 이 프로젝트에서는 **회원과 비회원 상태의 화면**만을 준비하고, 인증된 회원이면 회원용 화면을 띄운다. **그 밖의 화면들은 요구 작업을 수행하는 과정**에서 띄우므로 인증이 필요 없다.

### 대표 기능

- 끝말잇기 `싱글 게임` 플레이 중 제공되는 기능
  - `난이도는 10 레벨까지` 구현되어있으며, 각 레벨마다 사용되는 `기본 단어 목록`을 준비한다.
  - 컴퓨터의 데이터 학습 여부를 on으로 설정하면, 여태 실행된 모든 판에서 특정 회원이 입력한 단어(ok된 단어만)를 모든 난이도의 게임에서 사용한다.
  - `사용자가 게임 실패`하는 조건은
    - 시간초과 (1~3 : 8초, 4~7 : 5초, 8~10 : 3초)
    - 상대방이 제시한 단어의 끝글자와 앞글자가 다름
    - 이미 사용된 단어를 사용
  - `사용자가 게임에서 이기는 조건`은
    - 상대방이 이미 사용된 단어를 세번이상 뽑음(내부적으로)
    - 상대방이 적절한 단어가 없어 null를 리턴
  - `게임에서 이기면` 이어서 다음 레벨을 실행할 수 있으며, 이어 게임을 실행하지 않고 끝내면 사용자가 클리어한 가장 높은 레벨이 사용자의 데이터에 저장된다. (여태 클리어한 레벨보다 이번에 클리어한 레벨이 높으면 저장하는 방식)
  - `게임에서 지면` 같은 레벨을 다시 실행할 수 있으며, 이어 게임을 실행하지 않고 끝내면 사용자가 클리어한 가장 높은 레벨이 사용자의 데이터에 저장된다. (여태 클리어한 레벨보다 이번에 클리어한 레벨이 높으면 저장하는 방식)
  - `불러오기를 선택`하면 레벨 1부터 사용자가 클리어한 레벨까지 선택이 가능하다.
  - 설정에 들어가면 `상대방의 이름`을 정할 수 있다
- `로그인, 로그아웃`
- 메인 메뉴(회원, 비회원 화면)에서 `quit`을 입력하면 클라이언트와 연결이 끊어지고, `stop`을 입력하면 서버가 종료된다.
- `멀티게임`은 준비 중인 서비스이다.
- `관리자의 기능`으로 회원의 정보를 간단히 조회할 수 있다.

### 한계

### 클래스 구조

