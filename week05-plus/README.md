[전체 목차](../README.md) · [← 5주차](../week05/README.md) · [6주차 →](../week06/README.md)

# 5+주차 · 5+주차 확장 작업

5+주차 관련 저장소 두 곳을 함께 연결합니다. 작성자 커밋이 확인되는 CaptainTangerine 저장소를 설명의 기준으로 삼고, mathison0 저장소도 별도로 보존해 연결합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [CaptainTangerine/KraftonJungle3_Week5Plus_Team8](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8) | 공개 | [62a7cb9](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/tree/62a7cb9f18c30237ebba45adb63baec431f09e99) |
| [mathison0/Jungle_Week5plus_Team8](https://github.com/mathison0/Jungle_Week5plus_Team8) | 비공개 | [810118f](https://github.com/mathison0/Jungle_Week5plus_Team8/tree/810118fe784f3576f754f65ee430e83f9c4a77e6) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 에디터의 Add Component와 프로퍼티 편집
- PlayerStart의 선택·방향 표시와 PIE 시작 방향
- MovementComponent와 회전 처리

## 내 기여

에디터에서 액터를 조립하고, 편집한 상태를 PIE 실행으로 연결하는 부분을 담당했습니다. 아래 내용은 CaptainTangerine 원본의 `DDing-Ho` 작성 커밋과 실제 변경 파일을 기준으로 정리했습니다.

### 1. 클래스 등록 정보를 활용한 Add Component와 속성 편집

액터에 컴포넌트를 추가하는 작업을 에디터 안에서 처리할 수 있도록 Add Component 메뉴를 구현했습니다. `UClass`에 등록된 컴포넌트 클래스를 모아 표시 이름으로 정렬하고, 검색어 필터와 기본 클래스 제외 조건을 적용했습니다. 컴포넌트의 정확한 클래스 조회와 씬 로드 후 부모 UUID를 이용한 연결 복원도 함께 정리해, UI에서 추가한 컴포넌트와 저장된 계층 구조를 다루는 흐름을 연결했습니다.

근거: [Add Component·프로퍼티 편집 커밋](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/commit/4869fee76bc4d873bf059bb73fd1c694556d97ce) · [PropertyWindow.cpp](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/4869fee76bc4d873bf059bb73fd1c694556d97ce/Editor/Source/UI/PropertyWindow.cpp)

### 2. PlayerStart의 시작 방향 시각화와 컴포넌트 복원

배치한 PlayerStart가 어느 방향을 바라보는지 확인할 수 있도록 선분 메시 기반의 `ArrowComponent`를 추가했습니다. 화살표와 빌보드의 생성·부착을 공통 초기화 함수로 묶고, 씬을 불러온 뒤에도 시각화 컴포넌트를 다시 구성하도록 처리했습니다. 후속 작업에서는 로드된 컴포넌트의 Owner를 액터로 다시 설정해, PlayerStart 선택에 필요한 소유 관계를 복구했습니다.

근거: [방향 화살표 추가](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/commit/fea35338e9a73408a773dbe3d86f29fcfe4749b8) · [선택 복구](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/commit/5eec2e6b35d54d3e92e406fd6ed0c4007638763f) · [PlayerStart.cpp](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/fea35338e9a73408a773dbe3d86f29fcfe4749b8/Engine/Source/Actor/PlayerStart.cpp)

### 3. 편집 상태와 실행 상태를 구분한 MovementComponent

액터에 반복 이동을 부여하는 `MovementComponent`를 구현하고, 활성 여부·진폭·속도를 프로퍼티 창에서 조절하도록 연결했습니다. 이동은 Game·PIE 월드에서만 수행하고, 시작 높이를 기준으로 사인파 이동을 계산해 편집 중인 액터 위치와 실행 중의 움직임을 구분했습니다. 설정은 직렬화하되 경과 시간 같은 런타임 상태는 로드·복제 시 초기화하도록 처리했습니다.

근거: [MovementComponent 추가](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/commit/5eec2e6b35d54d3e92e406fd6ed0c4007638763f) · [MovementComponent.cpp](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/5eec2e6b35d54d3e92e406fd6ed0c4007638763f/Engine/Source/Component/MovementComponent.cpp)

### 4. 배치 방향과 PIE 카메라 시작 방향의 일치

PIE 카메라 회전을 PlayerStart의 월드 forward 축에서 계산하도록 바꿔, 시작 위치와 방향을 같은 월드 기준으로 가져오도록 정리했습니다. 정규화한 방향 벡터로 pitch·yaw를 구하고, 쿼터니언의 Rotator 변환도 정규화된 축과 직교 기저를 사용하는 방식으로 수정했습니다. 에디터 배치 결과가 실행 시작 카메라에 반영되는 경로와 엔진의 회전 변환을 함께 점검한 작업입니다.

근거: [회전 계산 수정](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/commit/6ea3aa74aba379bad428c919ee8889e18a70cb04) · [EditorEngine.cpp](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/6ea3aa74aba379bad428c919ee8889e18a70cb04/Editor/Source/EditorEngine.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/62a7cb9f18c30237ebba45adb63baec431f09e99/README.md)
- [5+주차 변경 사항](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/62a7cb9f18c30237ebba45adb63baec431f09e99/docs/2026-04-09_recent_changes.md)
- [Visual Studio 솔루션 · KraftonJungleEngine.sln](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/62a7cb9f18c30237ebba45adb63baec431f09e99/KraftonJungleEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/62a7cb9f18c30237ebba45adb63baec431f09e99/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8/blob/62a7cb9f18c30237ebba45adb63baec431f09e99/ReleaseBuild.bat)

이 페이지의 개인 기여는 CaptainTangerine 저장소의 커밋을 근거로 합니다. mathison0 저장소는 5+주차 관련 원본으로 함께 연결했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
