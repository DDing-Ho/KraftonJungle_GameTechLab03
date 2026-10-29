[전체 목차](../README.md) · [← 12주차](../week12/README.md) · [14주차 →](../week14/README.md)

# 13주차 · 물리·차량·카메라

물리 시뮬레이션과 차량 제어, 카메라 기능을 확장한 주차입니다. PhysX 차량 구조, Lua를 통한 탱크 조작과 카메라 DOF·파일럿 기능을 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [puter2712git/Jungle_Week13_Team3](https://github.com/puter2712git/Jungle_Week13_Team3) | 공개 | [bfd7c08](https://github.com/puter2712git/Jungle_Week13_Team3/tree/bfd7c08951dcc78d2687c15f5d9c760dad5564da) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- PhysX 차량 구조와 탱크 컴포넌트
- Lua 조작·터렛 제어와 주포 반동
- DOF·뷰포트 파일럿과 물리 통계

## 내 기여

차량 타입을 확장할 수 있는 PhysX 연동 구조와 Lua 제어 경로를 만들고, 카메라 편집 및 물리 상태를 관찰하는 도구를 구현했습니다. 아래는 `DDing-Ho` 작성 커밋으로 확인되는 작업이며, 팀의 물리 시스템 전체를 개인 구현으로 분류하지 않습니다.

### 1. 차량의 생성·갱신·해제와 타입별 구현 분리

4륜 차량에 묶여 있던 구조를 `UPhysXVehicleMovementComponent`와 `FPhysXVehicleInstanceBase`의 공통 인터페이스로 정리했습니다. 차량 매니저는 4륜 전용 래퍼 대신 PhysX의 `PxVehicleWheels`를 등록·갱신하게 바꿔, 다른 차량 타입도 같은 업데이트 흐름을 사용하도록 했습니다. 생성·등록·해제 책임을 공통화하면서 기존 컴포넌트 이름과 SetDriveInput·Lua 접근 API는 유지해 기존 씬과 제어 코드의 연결을 보존했습니다.

근거: [차량 구조 재구성 커밋](https://github.com/puter2712git/Jungle_Week13_Team3/commit/692892f3439d744ee39b28b5ae78a790482ade87) · [PhysXVehicleMovementComponent.cpp](https://github.com/puter2712git/Jungle_Week13_Team3/blob/692892f3439d744ee39b28b5ae78a790482ade87/KraftonEngine/Source/Engine/Component/Movement/PhysX/PhysXVehicleMovementComponent.cpp)

### 2. 탱크 컴포넌트·좌우 트랙 입력과 Lua 조작

`PxVehicleDriveTank` 기반의 차량 인스턴스와 이동 컴포넌트를 추가해 좌우 트랙 입력, WASD 주행 입력과 발사 반동의 충격량을 제공했습니다. Lua에서 탱크 컴포넌트를 얻는 API와 조작 예제를 연결하고, 스로틀·브레이크·조향 입력은 목표값으로 점진적으로 바뀌도록 처리했습니다. C++ 물리 동작과 스크립트 입력을 분리해, 게임 조작을 Lua에서 구성할 수 있는 연결점을 만들었습니다.

근거: [탱크·Lua 조작 커밋](https://github.com/puter2712git/Jungle_Week13_Team3/commit/a946c7a58838463ec04ca692dd831273e622654a) · [TankVehicle.lua](https://github.com/puter2712git/Jungle_Week13_Team3/blob/a946c7a58838463ec04ca692dd831273e622654a/KraftonEngine/Content/Script/TankVehicle.lua)

### 3. 배치 카메라를 직접 조작하는 뷰포트 파일럿

CameraActor·CineCameraActor를 에디터에 배치하고, 툴바에서 선택한 카메라의 시점으로 전환하는 파일럿 기능을 추가했습니다. 파일럿 상태에서는 뷰포트 입력을 카메라 액터에 적용하고, 해당 카메라의 아이콘·기즈모가 시야를 가리지 않도록 에디터 전용 렌더 데이터를 숨겼습니다. PIE 시작이나 씬 초기화 시에는 파일럿을 종료해 편집 대상과 플레이 시점이 뒤섞이지 않도록 연결했습니다.

근거: [카메라·파일럿 커밋](https://github.com/puter2712git/Jungle_Week13_Team3/commit/c1f410db3a3f23e15b4edb3835caefd6e0cce6bc) · [EditorViewportClient.cpp](https://github.com/puter2712git/Jungle_Week13_Team3/blob/c1f410db3a3f23e15b4edb3835caefd6e0cce6bc/KraftonEngine/Source/Editor/Viewport/EditorViewportClient.cpp)

### 4. 물리·래그돌·천의 상태를 확인하는 통계 도구

PhysX의 body·constraint·active actor·vehicle 수와 차량 업데이트·시뮬레이션·동기화·질의 구간의 CPU 시간을 수집하도록 했습니다. 래그돌·천 시뮬레이션에도 활성 개수와 주요 갱신 구간의 시간을 연결하고, `stat physx`, `stat ragdoll`, `stat cloth` 명령으로 개별 오버레이를 켤 수 있게 했습니다. 물리 기능을 화면에 구현하는 데서 더 나아가, 어떤 상태와 처리 구간을 점검할지 확인할 수 있는 관찰 도구를 추가한 작업입니다.

근거: [물리 통계 커밋](https://github.com/puter2712git/Jungle_Week13_Team3/commit/cd32a15eb054f264f4601858b491c1fbbd6b117e) · [PhysicsStats.h](https://github.com/puter2712git/Jungle_Week13_Team3/blob/cd32a15eb054f264f4601858b491c1fbbd6b117e/KraftonEngine/Source/Engine/Profiling/Stats/PhysicsStats.h)

## 문서와 실행 자료

- [스키닝 수정 기록](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/Docs/SkeletalMeshSkinningFixNotes.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
