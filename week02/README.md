[전체 목차](../README.md) · [← 1주차](../week01/README.md) · [3주차 →](../week03/README.md)

# 2주차 · 3D 엔진·에디터의 기초

Jungle Engine의 런타임과 에디터를 구성한 주차입니다. C++20, DirectX 11, Win32, ImGui를 바탕으로 씬·오브젝트·뷰포트와 편집 도구를 연결합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/Jungle3_Week2_Team1](https://github.com/DDing-Ho/Jungle3_Week2_Team1) | 공개 | [7dc690c](https://github.com/DDing-Ho/Jungle3_Week2_Team1/tree/7dc690cf0ff416596955a6c1b1be4ae1f75c9903) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- Engine·Editor·Client 실행 대상 분리
- 오브젝트·컴포넌트 구조와 씬 저장·복원
- 선택·기즈모·뷰포트와 카메라 조작

## 내 기여

씬 컨텍스트와 에디터 조작 도구를 중심으로 런타임·입력·렌더링을 연결했습니다. 아래 설명은 `DDing-Ho` 작성 커밋의 실제 변경 내용을 기준으로 정리한 개인 작업입니다.

### Game·Editor·Preview 씬 컨텍스트 분리

씬의 이름·유형·객체를 묶는 `FSceneContext`와 선택 액터 상태를 포함하는 에디터 컨텍스트를 도입했습니다. 코어에서 Game·Editor와 여러 Preview 컨텍스트의 생성·삭제·활성 전환을 관리하고, 시작할 씬 유형을 지정하도록 확장했습니다. Control Panel에서도 활성 컨텍스트를 확인·전환하고 프리뷰의 씬 저장·불러오기를 제한해, 편집 대상과 미리보기 대상의 역할을 구분했습니다.

근거: [씬 컨텍스트 도입 커밋](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/5ef09bd3b1e77dd3fc049fcc2ff1f3caf560c95e) · [SceneContext.h](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/5ef09bd3b1e77dd3fc049fcc2ff1f3caf560c95e/Engine/Source/Scene/SceneContext.h)

### 선택부터 드래그·렌더링까지 연결한 Transform 기즈모

이동·회전·크기 조절 기즈모에 축·평면 히트 테스트, hover 상태와 드래그 시작·갱신·종료 흐름을 구현했습니다. 마우스 레이와 평면·삼각형의 교차를 이용해 조작량을 계산하고, World·Local 좌표계와 액터의 상대 변환을 구분해 적용했습니다. 이를 `EditorViewportClient`의 입력 처리와 렌더 명령 생성에 연결하고, 조작 결과를 속성 UI에도 동기화해 뷰포트에서 선택한 오브젝트를 직접 편집할 수 있게 했습니다.

근거: [기즈모 입력·렌더링 구현 커밋](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/a9321626603bf0d6967435b55b65606d9fec47c4) · [Gizmo.cpp](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/a9321626603bf0d6967435b55b65606d9fec47c4/Editor/Source/Gizmo/Gizmo.cpp) · [EditorViewportClient.cpp](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/a9321626603bf0d6967435b55b65606d9fec47c4/Editor/Source/UI/EditorViewportClient.cpp)

### 직교 카메라에 맞춘 피킹·기즈모 크기 계산

카메라에 원근·직교 투영 모드와 직교 시야 크기 설정을 추가했습니다. 직교 모드에서는 화면 좌표에 따라 레이의 시작점을 옮기고 방향은 카메라 전방으로 유지하도록 피킹을 분기했으며, 기즈모 크기도 거리·FOV 대신 직교 시야 높이를 기준으로 계산했습니다. 카메라 투영만 바꾸는 데서 끝내지 않고 선택·변형 도구의 수학 처리와 설정 UI까지 함께 맞췄습니다.

근거: [직교 카메라·피킹 개선 커밋](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/7dc690cf0ff416596955a6c1b1be4ae1f75c9903) · [Picker.cpp](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/Editor/Source/Picking/Picker.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/README.md)
- [Visual Studio 솔루션 · KraftonJungleEngine.sln](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/KraftonJungleEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/ReleaseBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
