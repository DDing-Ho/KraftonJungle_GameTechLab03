[전체 목차](../README.md) · [← 8주차](../week08/README.md) · [10주차 →](../week10/README.md)

# 9주차 · 게임플레이·에디터 도구

CrashEngine에서 게임플레이와 에디터 도구를 함께 확장한 주차입니다. 카메라 셰이크의 패턴·편집·재생과 게임 UI, 콘텐츠 탐색 흐름을 중심으로 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [chodott/Jungle_Week9_Team2](https://github.com/chodott/Jungle_Week9_Team2) | 공개 | [a5aeee8](https://github.com/chodott/Jungle_Week9_Team2/tree/a5aeee8d58b47a3efc69bb75541ad666a2f74990) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 패턴 기반 카메라 셰이크
- 시퀀스 카메라 셰이크 편집과 게임플레이 재생
- Output Log·Content Browser와 Lua 스크립트 탐색

## 내 기여

카메라 셰이크를 작성·편집·저장하고 게임에서 재생하는 흐름과 Lua UI 개선을 담당했습니다. 아래 항목은 팀 전체 게임 기능과 구분해, `DDing-Ho` 작성 커밋과 실제 변경 파일에서 확인되는 작업을 설명합니다.

### 1. 재생 상태와 흔들림 계산을 나눈 패턴 기반 구조

카메라 셰이크의 수명·블렌드 인·아웃을 관리하는 상태와, 위치·회전·FOV 오프셋을 만드는 패턴을 분리했습니다. 시작·업데이트·스크럽·중지의 공통 인터페이스를 두고, 축별 진폭·주파수로 동작하는 WaveOscillator 패턴을 연결했습니다. 흔들림 종류가 달라져도 공통 재생 흐름을 사용하고, 특정 시점의 결과를 편집기에서 평가할 수 있는 구조를 마련했습니다.

근거: [패턴 기반 셰이크 구현](https://github.com/chodott/Jungle_Week9_Team2/commit/2f6bbfd1b14a51724d7e7f30cbb3582f574b281b) · [CameraShakePattern.h](https://github.com/chodott/Jungle_Week9_Team2/blob/2f6bbfd1b14a51724d7e7f30cbb3582f574b281b/CrashEngine/Source/Engine/Camera/Shakes/CameraShakePattern.h)

### 2. 시퀀스 곡선 에디터와 셰이크 에셋 관리

위치 XYZ·회전·FOV 채널을 키와 핸들로 편집하는 시퀀스 카메라 셰이크 에디터를 구현했습니다. 에디터 패널에서 에셋 목록·새 에셋·저장·다른 이름으로 저장·미리보기를 다루고, `CameraShakeAssetManager`가 에셋 정의를 읽고 실제 셰이크 인스턴스로 만드는 흐름을 연결했습니다. 곡선 편집 결과를 `.shake` 에셋으로 보관해 런타임에서도 같은 정의를 사용할 수 있도록 구성했습니다.

근거: [시퀀스 셰이크 에디터·에셋 구현](https://github.com/chodott/Jungle_Week9_Team2/commit/a8718f15352c63e519c34d66fc552eeec4940f39) · [EditorCameraShakePanel.h](https://github.com/chodott/Jungle_Week9_Team2/blob/a8718f15352c63e519c34d66fc552eeec4940f39/CrashEngine/Source/Editor/UI/EditorCameraShakePanel.h) · [CameraShakeAssetManager.h](https://github.com/chodott/Jungle_Week9_Team2/blob/a8718f15352c63e519c34d66fc552eeec4940f39/CrashEngine/Source/Engine/Camera/Shakes/CameraShakeAssetManager.h)

### 3. Lua 게임 이벤트에서 에셋 기반 셰이크 재생

게임 스크립트가 에셋 경로와 강도를 넘겨 흔들림을 재생할 수 있도록 Lua API와 공통 `CameraShake` 모듈을 추가했습니다. GameViewportClient에서 현재 카메라의 기본 POV에 CameraManager의 결과를 적용하고, 적용했던 오프셋은 다음 입력·업데이트 전에 되돌리는 경로를 구성했습니다. 무기·폭발 같은 게임 이벤트가 에디터에서 만든 셰이크 에셋을 호출하도록 연결해, 연출 데이터와 게임 로직을 분리했습니다.

근거: [게임플레이 재생 연결](https://github.com/chodott/Jungle_Week9_Team2/commit/e44be78f34aec1ecbe255ca438f644a9a590ae27) · [CameraShake.lua](https://github.com/chodott/Jungle_Week9_Team2/blob/e44be78f34aec1ecbe255ca438f644a9a590ae27/CrashEngine/Asset/Scripts/Core/CameraShake.lua) · [GameViewportClient.cpp](https://github.com/chodott/Jungle_Week9_Team2/blob/e44be78f34aec1ecbe255ca438f644a9a590ae27/CrashEngine/Source/Engine/Viewport/GameViewportClient.cpp)

### 4. 선택지와 결과를 읽기 쉽게 구성하는 Lua UI

레벨업 선택창과 스코어보드의 표현을 공통 `UIStyle` 모듈로 정리했습니다. 무기 아이콘·설명·업그레이드 전후 수치의 표기와 색상 규칙을 모으고, 선택 카드의 상태와 결과 순위에 맞는 표현을 각 UI에 적용했습니다. 게임 데이터에서 필요한 정보를 가져와 UI에 표시하는 구조를 보강해, 레벨업 선택과 게임 결과를 확인하는 화면을 개선했습니다.

근거: [레벨업·스코어보드 UI 개선](https://github.com/chodott/Jungle_Week9_Team2/commit/b3e819c0e4cefd864c00158d655457663003c7cc) · [UIStyle.lua](https://github.com/chodott/Jungle_Week9_Team2/blob/b3e819c0e4cefd864c00158d655457663003c7cc/CrashEngine/Asset/Scripts/UI/UIStyle.lua)

관련 PR: [에디터 드로어·Output Log·Lua 탐색 PR](https://github.com/chodott/Jungle_Week9_Team2/pull/1)

## 문서와 실행 자료

- [Visual Studio 솔루션 · CrashEngine.sln](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/CrashEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/GenerateProjectFiles.bat)
- [EditorBuild.bat](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/EditorBuild.bat)
- [GameBuild.bat](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
