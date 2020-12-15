﻿# 10조 Final Project

**조원** : 도건희, 정호성, 김규민, 사윤수

# 게임 스토리

재림의 코딩 고수가 되기 위해서 걸어가야 하는 길은 험난하다. 이 왕도를 걷고자 하는 이에게 연습은 피가 되고 살이 되는 일일 것이다. 그러나 이 과정에서 필수적으로 수반되는 일이 있으니, 그것은 바로 터미널에 아로새겨지는 'error'라는 글자이다. 코린이는 발생한 'error'를 해결함으로써 코딩 능력을 향상시켜야만 한다.
이 일련의 과정이 머드게임의 뼈대이다. 유저는 프로젝트를 완성하기 위해 경험치를 쌓고 버그를 해결해야 한다. 해당 경험치는 필드 위에 있는 'error'들로부터 넉다운되지 않고 그것들을 물리침으로써 얻을 수 있다. 프로젝트를완성하기 위한 여정을 함께 즐겨주기를 발란다.

# 구성 설명

## 기본 구성

express, mongoose를 활용하였으며, 상태의 변화는 별도의 데이터베이스에 실시간으로 저장한다. 아이템, 맵 등의 정보는 json 형태로 서버에서 따로 보관한다. 	
### datas
* constantManager : constants.json 파일을 받아옴, gameName 저장
* mapManager : map.json 파일을 받아옴, id, field!
* monsterManager : monsters.json 파일을 받아옴 monster 내용 저장
* itemManager : items.json 파일을 받아옴 item 내용 저장
* eventManager : events.json 파일을 받아옴

### models
* Player : player의 기본 스펙 및 레벨업 

## 구현된 기본 스펙

모든 행동들은 서버에서 이루지며, 클라이언트에서 별도로 확인이 가능하다.

* 온라인 플레이 가능
* 로그인, 회원가입 기능
* 10*10의 맵
* 캐릭터 이동 가능
* 이동 시 필드 별로 다음과 같은 일이 발생한다
1) 아무 일도 일어나지 않음
2) 전투 발생
3) 아이템 획득
* 5종 이상의 몬스터
1) 콜백 헬
  **HP**: 10
   **공격력**: 5
   **방어력**: 5
   **경험치**: 10
2) 하드코딩
  **HP**: 20
   **공격력**: 15
   **방어력**: 5
   **경험치**: 30
3) 스파게티 코드
  **HP**: 20
   **공격력**: 5
   **방어력**: 15
   **경험치**: 30
4) 컴파일 에러
  **HP**: 20
   **공격력**: 5
   **방어력**: 15
   **경험치**: 50
5) 강제종료 (BOSS)
  **HP**: 50
   **공격력**: 30
   **방어력**: 30
   **경험치**: 100
   **출현조건**: *????*

* 5종 이상의 아이템
1) 손목 보호대
방어력+ 5
2) 블루라이트 안경
방어력 + 5
3) 시디즈 의자
방어력 + 10
4) 스택오버플로우
공력력 + 15 방어력 + 15
5) 알코올
공격력 - 5
방어력 - 5
6) 니코틴
공격력 + 10
7) 카페인
방어력 + 10
8) 진님의 은총
공격력 + 10, 방어력 + 10

### 캐릭터의 기본 설정
1) 기본 HP : 30
2) 기본 공격력(str) : 10
3) 기본 방어력 (def) : 10
4) 기본 달성 경험치 : 20, 레벨 증가시 10씩 추가

### 전투 시스템
공격력과 방어력은 서로를 cancel out하는 성질을 가진다. 예를 들어, 유저 캐릭터의 공격력이 10이고 몬스터의 방어력이 10일 때는 '10-10=0'이 되어 데미지가 들어가지 않는다. 따라서 레벨업 또는 아이템 착용을 통하여 공격력을 상승시키지 않으면 몬스터에게 데미지를 줄 수 없다. 이는 몬스터가 유저 캐릭터를 공격할 때도 마찬가지이다. 

### 사망 시스템
전투 도중 HP가 0이 되면 캐릭터는 사망하고, (0,0) 위치로 소환된다.

### 레벨 시스템
캐릭터는 레벨업을 할 때마다 다음과 기본 설정 스펙에 다음과 같은 추가 스펙을 얻는다.
1) HP + 20
2) 공격력 + 5
3) 방어력 + 5
4) 다음 레벨 달성을 위해 필요한 경험치 + 10


## 구현된 추가 스펙
- 체력회복하는 이벤트가 추가된다.
- 필드에서 일어나는 이벤트 중 랜덤이벤트가 존재한다.
- 아이템을 소유할 경우, 캐릭터의 능력치가 향상된다. 능력치가 클라이언트에서 확인이 가능하다.
- 사망시 랜덤하게 아이템을 잃어버린다.
- 유저의 인벤토리가 클라이언트 상에서 확인이 가능하다.

## 진행 과정
- 김규민: 스토리 구성, event관리하는 함수 리팩토링
- 도건희: 뼈대 갖추기(git repository 생성, skeleton 적용), 일감 분배 및 전반적 리팩토링
- 사윤수: 아이템 랜덤 드랍기능 구현, test를 통한 버그 수정
- 정호성: Manager, constants 및 기본 함수들 구현 + 이미지 적용

## Trouble Shooting
1. 클라이언트의 출력 문제
- 이벤트의 text가 한줄로 쭉 나오고 있었는데, "<div></div>"로 묶여있는 것을 "<pre></pre>"로 바꿔서 해결
2. 순환참조 문제
- utils.js와 Manager등 import시에 서로 충돌이 생기는 경우가 발생. 이로 인해 함수 호출이 원활히 안됐음
- 순환참조를 없애고 import를 간결히 하여 문제 해결
3. slice와 splice 문제
- 아이템 랜덤 드랍시 array에서 해당 element를 삭제할때 원하는 대로 구현이 안됨.
- splice를 쓴줄 알고 계속 머리를 싸매다가 slice임을 발견
- slice는 기존의 array를 수정하지 않는다는 것을 확인.
- p 한글자에 시간을 뺏긴게 매우 허탈했음.
