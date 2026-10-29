[전체 목차](../README.md) · [← 5+주차](../week05-plus/README.md) · [7주차 →](../week07/README.md)

# 6주차 · 데칼·높이 안개

깊이·노말 데이터를 활용하는 화면 효과와 충돌 기반 게임플레이를 확장한 주차입니다. 팀 구현 문서에는 Decal, Fireball, Exponential Height Fog와 관련 에디터 기능이 정리되어 있습니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [esc10946/Jungle_Week6_Team6](https://github.com/esc10946/Jungle_Week6_Team6) | 공개 | [4285aef](https://github.com/esc10946/Jungle_Week6_Team6/tree/4285aef390ae572bfa2433b92a039ee4ef13b397) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- Projection Decal과 충돌 지점의 데칼 생성
- 깊이 버퍼를 이용한 월드 위치 복원
- Exponential Height Fog와 효과 통계·표시 제어

## 내 기여

팀의 화면 공간 효과 확장 작업에서 높이 안개의 셰이더·컴포넌트·렌더링 연결과 효과 통계 보완을 담당했습니다. 아래 설명은 `DDing-Ho` 작성 커밋의 실제 변경을 기준으로 하며, 팀의 Decal·Fireball 전체 구현과 구분합니다.

### 1. 깊이 버퍼에서 월드 위치를 복원하는 높이 안개 셰이더

화면에 그려진 깊이를 역투영·역뷰 행렬로 월드 위치로 복원하고, 카메라에서 해당 위치까지의 안개 밀도를 적분하는 Exponential Height Fog를 구현했습니다. 높이에 따른 밀도 감쇠와 시작·종료·차단 거리, 최대 불투명도를 파라미터로 다루도록 구성했습니다. 별도 안개 메시를 배치하는 대신 풀스크린 삼각형을 그리는 후처리 패스로 화면에 효과를 합성했습니다.

근거: [높이 포그 렌더링 추가](https://github.com/esc10946/Jungle_Week6_Team6/commit/8bb9917a421a65f1653c7c12efdaea6b585c5da5) · [HeightFogPostProcess.hlsl](https://github.com/esc10946/Jungle_Week6_Team6/blob/8bb9917a421a65f1653c7c12efdaea6b585c5da5/KraftonEngine/Shaders/HeightFogPostProcess.hlsl)

### 2. 효과의 배치·편집·저장과 렌더 실행 경로 연결

`ExponentialHeightFogComponent`를 씬에 등록·해제하고, RenderCollector가 읽은 효과 설정을 RenderBus를 거쳐 Renderer로 전달하도록 연결했습니다. 안개 파라미터는 프로퍼티 편집과 직렬화를 지원하고, 편집·로드 시 값의 범위를 보정하도록 처리했습니다. 렌더 단계에서는 원근 뷰에서 효과를 실행하고, 깊이 텍스처를 읽을 때의 바인딩 전환과 패스 종료 후 정리까지 포함해 엔진의 기존 렌더 흐름에 통합했습니다.

근거: [컴포넌트·렌더 경로 연결](https://github.com/esc10946/Jungle_Week6_Team6/commit/8bb9917a421a65f1653c7c12efdaea6b585c5da5) · [ExponentialHeightFogComponent.cpp](https://github.com/esc10946/Jungle_Week6_Team6/blob/8bb9917a421a65f1653c7c12efdaea6b585c5da5/KraftonEngine/Source/Engine/Component/ExponentialHeightFogComponent.cpp) · [Renderer.cpp](https://github.com/esc10946/Jungle_Week6_Team6/blob/8bb9917a421a65f1653c7c12efdaea6b585c5da5/KraftonEngine/Source/Engine/Render/Pipeline/Renderer.cpp)

### 3. 효과를 관찰할 수 있는 통계와 구현 문서 보완

Decal 오버레이에 개수 통계뿐 아니라 수집·렌더·합계 시간을 표시하도록 보완했습니다. CPU 통계 스냅샷에서 이름과 카테고리로 항목을 찾아 밀리초 단위로 보여주고, 콘솔의 `stat decal` 안내도 실제 동작에 맞췄습니다. 높이 안개는 파라미터·좌표 복원·렌더 패스의 연결 구조를 별도 문서로 남겨, 화면 결과를 수정할 때 관련 실행 경로를 찾아볼 수 있도록 정리했습니다.

근거: [Decal 통계 보완](https://github.com/esc10946/Jungle_Week6_Team6/commit/4b5caf0ff7a95d0e79215669aaa8b15b0a651551) · [OverlayStatSystem.cpp](https://github.com/esc10946/Jungle_Week6_Team6/blob/4b5caf0ff7a95d0e79215669aaa8b15b0a651551/KraftonEngine/Source/Editor/Subsystem/OverlayStatSystem.cpp) · [높이 안개 문서 작성](https://github.com/esc10946/Jungle_Week6_Team6/commit/fa29bc6673182c7a2ae17e062156d0d5f0a4aae9)

## 문서와 실행 자료

- [팀 구현 요약](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/Docs/W06_Team6_%EC%9E%A5%EB%AF%BC%EC%A4%80%EA%B0%95%EB%AA%85%ED%98%B8%EA%B9%80%ED%98%B8%EC%A4%80%EC%A1%B0%ED%98%84%EC%84%9D.md)
- [높이 안개 구현 문서](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/Docs/exponential-height-fog.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/ReleaseBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
