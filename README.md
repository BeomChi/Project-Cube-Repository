# Project Cube

> [!NOTE]
> 본 프로젝트는 팀 프로젝트로 진행되어
> Repository는 Private으로 유지하고 있습니다.
>
> 본 저장소는 프로젝트 소개와
> 제가 담당한 구현 내용을 정리하기 위한
> 포트폴리오 Repository입니다.

Unity를 활용하여 제작한 2인 팀 프로젝트입니다.

저는 해당 프로젝트에서 
플레이어와 몬스터의 전투 시스템, 버프 시스템,
FSM 기반 AI 등을 구현했습니다.


![플레이어 움직이는 거](/Image/PlayerMovement.gif)
![몬스터 패턴 1](/Image/MonsterAttack.gif)
![몬스터 공격 후 대치상태 후 다시 공격](/Image/MonsterFSM.gif)

## 개발 환경

Engin : Unity
Language : C#
Platform : Windows

## 담당 역할

Player
Monster AI
Buff System

## 프로젝트 구조

![전체 구조도](/Image/ProjectCube-페이지-15.drawio.png)

## Entity

Player와 Monster가 공통으로 사용하는 데이터와 기능을 관리하는 부모 클래스

공통 기능을 Entity에서 관리하고 Player와 Monster가 상속받도록 구성하여
중복 코드를 줄이고 객체별 기능에 집중할 수 있도록 했습니다.

![Entity 구조도](/Image/ProjectCube-Entity_1.drawio.png)
![Entity 구조도](/Image/ProjectCube-Entity_2.drawio.png)

## PlayerSysyem

입력 / 이동 / 공격 / 애니메이션을 각각 별도의 스크립트로 분리하여
역할별 책임을 나누었습니다.

Entity를 상속받아 체력, 스탯 등의 공통 기능을 재사용하고,
직업별 행동은 개별 스크립트에서 구현했습니다.

![플레이어 구성 구조도](/Image/ProjectCube-PlayerSystem.drawio.png)

![기본 캐릭터 이동 및 회피](/Image/PlayerMovement.gif)
![마법사 이동 및 회피](/Image/Wizard.gif)
![암살자 이동 및 회피](/Image/Assasin.gif)

## WeaponBase

초기에는 Coroutin과 normalizedTime을 이용해 공격 판정을 제어했습니다.
하지만 애니메이션이 변경될 때마다 코드도 함께 수정해야 하는 문제가 있었습니다.

이를 개선하기 위해 Animation Property에서 직접 공격 판정을 제어하도록 변경하여
애니메이션과 코드의 결합도를 낮췄습니다.

![개선전 후 구조도](/Image/ProjectCube-WeaponBase1.drawio.png)
![개선전 후 구조도](/Image/ProjectCube-WeaponBase2.drawio.png)
![에디터에서 실행하는 gif](/Image/weaponBase.gif)


## AttackPattern

몬스터의 공격 정보를 AttackPattern 구조체로 관리했습니다.

각 공격은
 - 쿨타임
 - 스태미나
 - 호출 함수

등의 정보를 하나의 데이터로 관리합니다.

등록된 AttackPattern을 기반으로 Reflection을 이용하여
공격 함수를 실행하도록 구현했습니다.

 - 공격 정보를 데이터로 관리
 - 새로운 공격 추가가 용이
 - 몬스터별 공격 조합 가능

![Attack Pattern 구조도](/Image/ProjectCube-AttackPattern1.drawio.png)
![Attack Pattern 구조도](/Image/ProjectCube-AttackPattern2.drawio.png)
![Attack Pattern 구조도](/Image/ProjectCube-AttackPattern3.drawio.png)

## Monster AI

FSM을 기반으로 몬스터의 상태와 전투 행동을 구현했습니다.

- Patrol
- Chase
- Attack
- Standoff

### Monster Patterns

몬스터별 공격 패턴을 구현하여 서로 다른 전투 방식을 구성했습니다.

![몬스터 공격 패턴 GIF](/Image/MonsterAttack.gif)

![공격 → 대치 → 재공격 GIF](/Image/MonsterFSM.gif)

## 해당 프로젝트를 통해 무엇을 배웠나?

- 플레이어와 몬스터의 공통 기능을 분리하는 방법을 배웠습니다.
- 애니메이션과 코드의 결합도를 줄이는 방법을 경험했습니다.
- 팀 프로젝트에서 역할을 나누어 협업하는 경험을 했습니다.
- 현재 다시 구현한다면 Reflection 대신 Delegate나 Interface 기반 구조도 고려해보고 싶습니다.