[전체 목차](../README.md) · [← 13주차](../week13/README.md)

# 14주차 · 정글무쌍 게임잼

과정에서 개발한 KraftonEngine 위에서 만든 3D 핵앤슬래시 게임 「정글무쌍」의 팀 프로젝트입니다. 원본에는 과정 전체의 공동 엔진 코드와 게임잼의 게임 코드·콘텐츠가 함께 있습니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [puter2712git/Jungle_Week14_Team2](https://github.com/puter2712git/Jungle_Week14_Team2) | 공개 | [da1f896](https://github.com/puter2712git/Jungle_Week14_Team2/tree/da1f8960cd3a03a1a1bd18e95599831f00f112db) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 군중 전투와 유닛의 추종·소환
- 중간보스·최종보스와 게임 진행
- 보스 조우·공격·사망 연출과 아웃트로

## 내 기여

게임잼에서는 군중 유닛 관리·교전 흐름과 최종 보스의 조우·사망 연출을 구현했습니다. 과정 전체가 함께 개발한 엔진과 팀의 게임 결과물 위에서 작업했으며, 아래는 `DDing-Ho` 작성 커밋으로 확인되는 개인 변경 범위입니다.

### 1. 컴포넌트 기반 군중 관리와 Lua 연결

대규모 유닛 관리 흐름을 Actor 전용 구조에서 `ULargeScaleUnitManagerComponent`로 옮기고, 유닛 핸들·아키타입·이동·공간 질의·공격·데미지 처리를 컴포넌트에서 관리하도록 구성했습니다. Lua의 `Crowd.GetOrCreateManager(ownerActor)`는 월드의 기존 매니저를 재사용하거나 지정 액터에 컴포넌트를 붙이게 해, 게임 스크립트에서 군중 시스템을 사용할 수 있도록 했습니다. BeginPlay 중 컴포넌트가 추가되는 상황에 맞춰 액터의 순회 방식도 보강했습니다.

근거: [군중 관리 컴포넌트 커밋](https://github.com/puter2712git/Jungle_Week14_Team2/commit/5475cbdfec4493bcbd7e662278c8bc2b94203be6) · [LargeScaleUnitManagerComponent.cpp](https://github.com/puter2712git/Jungle_Week14_Team2/blob/5475cbdfec4493bcbd7e662278c8bc2b94203be6/KraftonEngine/Source/Game/Crowd/LargeScaleUnitManagerComponent.cpp)

### 2. 거리 LOD·교전 제한과 밀집 이동 문제 보완

플레이어와의 거리에 따라 유닛의 시뮬레이션 빈도와 비주얼 처리를 조절하는 LOD를 추가하고, 근접·원거리 링 슬롯과 Attack Token으로 동시 공격 수를 제어하도록 했습니다. 밀집 구간에서는 같은 팀 유닛을 soft blocker로 처리하고 옆걸음 후보·타겟 재평가·분리 속도 smoothing을 적용해 이동 막힘과 떨림을 완화하는 로직을 보강했습니다. 스포너에는 초기 이동 목표와 누적 소환 상한을 추가하고, 지연 스폰에서도 목표가 유지되도록 해 전장의 유입 방향과 생성량을 스크립트에서 설정할 수 있게 했습니다.

근거: [LOD·교전 AI](https://github.com/puter2712git/Jungle_Week14_Team2/commit/f3fb67c6beba74f12b191900b5469539ec7d6002) · [밀집 이동 보완](https://github.com/puter2712git/Jungle_Week14_Team2/commit/3a29177fdb6d4a59fdcd35a2f7d6ade6f164dbb9) · [이동 목표·소환 제한](https://github.com/puter2712git/Jungle_Week14_Team2/commit/24cfc783476058224e0af75f3aedaf6e58870423) · [CrowdEngagementManager.cpp](https://github.com/puter2712git/Jungle_Week14_Team2/blob/f3fb67c6beba74f12b191900b5469539ec7d6002/KraftonEngine/Source/Game/Crowd/CrowdEngagementManager.cpp)

### 3. 중간보스 이후의 최종 보스 조우 시퀀스

중간보스 제거를 기다린 뒤 다이얼로그와 최종 보스의 기상·포효 애니메이션을 순서대로 진행하는 조우 매니저를 추가했습니다. 연출 중에는 플레이어 입력·HUD·카메라를 제어하고, 연출이 끝나면 보스 무적을 해제하고 전투 패턴을 시작하도록 단계별 흐름을 연결했습니다. 최종 보스 전용 매니저와 게임모드 API를 통해 전투 진입을 구성했습니다.

근거: [최종 보스 조우 커밋](https://github.com/puter2712git/Jungle_Week14_Team2/commit/265083a0dafdb9586f53b500f0a82c9ea6f70717) · [MainBossEncounterManager.cpp](https://github.com/puter2712git/Jungle_Week14_Team2/blob/265083a0dafdb9586f53b500f0a82c9ea6f70717/KraftonEngine/Source/Game/Musou/MainBoss/MainBossEncounterManager.cpp)

### 4. 보스 사망 상태에서 승리·아웃트로까지 연결

보스의 체력이 소진되면 기존 패턴과 이동을 정리하고 별도의 사망 상태로 전환하도록 했습니다. 사망 애니메이션의 재생 시간이 지난 뒤 기존 `NotifyVictory` 흐름을 호출해 아웃트로와 승리 UI로 이어지게 하고, 아웃트로 시작 여부를 따로 보관해 중복 호출을 막았습니다. 전투 종료가 단순 액터 제거로 끝나지 않고 팀이 만든 게임 진행·결과 화면과 연결되도록 마무리한 작업입니다.

근거: [사망·아웃트로 커밋](https://github.com/puter2712git/Jungle_Week14_Team2/commit/729c129bbd8eb21ed403ee38c25cda51204ad980) · [MainBossPatternComponent.cpp](https://github.com/puter2712git/Jungle_Week14_Team2/blob/729c129bbd8eb21ed403ee38c25cda51204ad980/KraftonEngine/Source/Game/Musou/MainBoss/MainBossPatternComponent.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/puter2712git/Jungle_Week14_Team2/blob/da1f8960cd3a03a1a1bd18e95599831f00f112db/README.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/puter2712git/Jungle_Week14_Team2/blob/da1f8960cd3a03a1a1bd18e95599831f00f112db/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/puter2712git/Jungle_Week14_Team2/blob/da1f8960cd3a03a1a1bd18e95599831f00f112db/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/puter2712git/Jungle_Week14_Team2/blob/da1f8960cd3a03a1a1bd18e95599831f00f112db/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/puter2712git/Jungle_Week14_Team2/blob/da1f8960cd3a03a1a1bd18e95599831f00f112db/GameBuild.bat)

## 시연 영상

[정글무쌍 플레이 영상 보기](https://youtu.be/-prBOp3srOc)

원본 README에 연결된 팀 시연 영상입니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
