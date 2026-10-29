[전체 목차](../README.md) · [← 2주차](../week02/README.md) · [4주차 →](../week04/README.md)

# 3주차 · CO-PASS Engine

Win32, Direct3D 11, ImGui 기반의 CO-PASS Engine을 개발한 주차입니다. 에셋 로딩과 캐시, 패널 시스템, Content Browser를 중심으로 편집 흐름을 확장합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/KraftonJungle3_Week3_Team2](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2) | 공개 | [a587fc1](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/tree/a587fc19e11341b3ee1509e7d3a408ded82f8f7e) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- AssetManager와 로더·캐시
- 패널 기반 에디터 UI와 Console
- Content Browser의 인덱싱과 드래그 앤 드롭

## 내 기여

에셋을 불러오는 엔진 계층과 에셋을 탐색·지정하는 에디터 계층을 함께 개발했습니다. 아래 설명은 `DDing-Ho` 작성 커밋의 실제 변경 내용을 기준으로 정리한 개인 작업입니다.

### 로더를 확장할 수 있는 에셋 로딩·캐시 구조

파일을 읽는 책임을 `IAssetLoader`로 분리하고, `UAssetManager`가 등록된 로더 중 경로·에셋 유형에 맞는 로더를 선택하도록 구현했습니다. 정규화 경로·에셋 유형·빌드 옵션 서명으로 캐시 키를 만들고, 원본 해시가 일치하면 로드된 에셋을 재사용하도록 구성했습니다. 강제 재로딩과 캐시 무효화 경로도 두어, 파일 형식별 로딩 코드와 공통 캐시 정책을 나눴습니다.

근거: [에셋 로더·캐시 구현 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/0034a457316853fa32082a6fe3dc6a44657083a0) · [AssetManager.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/0034a457316853fa32082a6fe3dc6a44657083a0/Engine/Source/Engine/Asset/AssetManager.cpp)

### 공통 컨텍스트를 사용하는 패널 인터페이스

`IPanel`에 초기화·열기·닫기·Tick·Draw의 공통 인터페이스를 두고, `FPanelManager`가 등록한 패널을 갱신·그리도록 초기 구조를 작성했습니다. 씬·RHI·에셋 매니저·선택 오브젝트는 `FEditorContext`로 전달해 각 패널이 편집에 필요한 상태를 같은 방식으로 참조하게 했습니다. 에디터 창이 늘어날 때 입력 데이터와 공통 수명주기를 연결할 기반을 마련한 작업입니다.

근거: [패널·컨텍스트 추가 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/5c8b4450d68e10f92de5d6096ed017ec86c35922) · [Panel.h](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/5c8b4450d68e10f92de5d6096ed017ec86c35922/Editor/Source/Panel/Panel.h) · [PanelManager.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/5c8b4450d68e10f92de5d6096ed017ec86c35922/Editor/Source/Panel/PanelManager.cpp)

### 콘텐츠 인덱스와 탐색 UI 분리

`/Game` 콘텐츠를 스캔해 폴더·파일 정보를 스냅샷으로 보관하는 `FEditorContentIndex`와 이를 표시하는 `FContentBrowserPanel`을 구현했습니다. 폴더 트리, 파일 목록, 검색·유형 필터와 폭 조절 패널을 제공하고, 왼쪽 패널 폭을 에디터 설정으로 저장하도록 연결했습니다. 파일 탐색 데이터와 ImGui 표현을 나눠, 에셋을 찾는 흐름을 독립된 에디터 도구로 구성했습니다.

근거: [Content Browser 구현 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/77b00462214feb23db39ce4fda43d47e58ac2780) · [EditorContentIndex.h](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/77b00462214feb23db39ce4fda43d47e58ac2780/Editor/Source/Content/EditorContentIndex.h) · [ContentBrowserPanel.h](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/77b00462214feb23db39ce4fda43d47e58ac2780/Editor/Source/Panel/ContentBrowserPanel.h)

### 에셋 유형을 검사하는 드래그 앤 드롭

Content Browser에서 텍스처·폰트 등을 끌어와 Properties의 에셋 경로 항목에 지정하는 흐름을 연결했습니다. 드래그 데이터에 가상 경로와 에셋 유형을 담고, 대상 프로퍼티가 요구하는 유형과 호환될 때만 setter와 편집 버퍼에 반영하도록 구현했습니다. 파일을 찾는 단계와 컴포넌트에 적용하는 단계를 연결하면서, 맞지 않는 유형의 에셋이 드롭되는 경우를 처리했습니다.

근거: [드래그 앤 드롭 구현 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/643f51c9493c9df6b1b29854c9a7ef2132a14629) · [ContentBrowserDragDrop.h](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/643f51c9493c9df6b1b29854c9a7ef2132a14629/Editor/Source/Content/ContentBrowserDragDrop.h) · [PropertiesPanel.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/643f51c9493c9df6b1b29854c9a7ef2132a14629/Editor/Source/Panel/PropertiesPanel.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/a587fc19e11341b3ee1509e7d3a408ded82f8f7e/README.md)
- [Visual Studio 솔루션 · Kraftonjungle_Team2.sln](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/a587fc19e11341b3ee1509e7d3a408ded82f8f7e/Kraftonjungle_Team2.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/a587fc19e11341b3ee1509e7d3a408ded82f8f7e/GenerateProjectFiles.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
