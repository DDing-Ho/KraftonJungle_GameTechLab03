[전체 목차](../README.md) · [← 6주차](../week06/README.md) · [8주차 →](../week08/README.md)

# 7주차 · 조명·셰이더 파이프라인

NipsEngine의 셰이더 바인딩과 조명 경로를 확장한 주차입니다. 셰이더 리플렉션을 통한 파라미터 업로드, UberLit 기반 조명 처리와 하늘 렌더링을 중심으로 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [jskim-research/Jungle_Week7_Team4](https://github.com/jskim-research/Jungle_Week7_Team4) | 공개 | [b076888](https://github.com/jskim-research/Jungle_Week7_Team4/tree/b0768887dd289b005042df80afeacb7e2a0b7d63) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 셰이더 리플렉션 기반의 렌더 파라미터 연결
- 전방 조명과 UberLit 셰이더
- 조명 반응형 데칼과 SkyAtmosphere

## 내 기여

셰이더 파라미터를 전달하는 공통 구조와 이를 사용하는 머티리얼·렌더 패스를 담당했습니다. `DDing-Ho` 작성 커밋에서 확인되는 리플렉션 바인딩, Uber 셰이더, 데칼 조명과 하늘 패스 작업을 정리했습니다.

### 1. 셰이더 리플렉션 기반의 공통 바인딩 구조

렌더 패스에서 직접 지정하던 상수 버퍼와 리소스 바인딩을 셰이더 리플렉션 정보와 `FShaderBindingInstance`를 사용하는 구조로 옮겼습니다. 셰이더 단계별로 상수 버퍼의 크기·변수 오프셋, 텍스처·샘플러의 바인딩 위치를 수집하고, 이름 기반 파라미터 설정 API로 연결했습니다. 머티리얼뿐 아니라 FXAA·Fog·Selection Mask 등의 렌더 패스도 같은 경로를 사용하도록 바꿔, 셰이더별 데이터 전달 방식을 공통화했습니다.

근거: [바인딩 시스템 이관](https://github.com/jskim-research/Jungle_Week7_Team4/commit/e7f10bc3e738a8882fd2674e532216b1a7518d2d) · [Shader.h](https://github.com/jskim-research/Jungle_Week7_Team4/blob/e7f10bc3e738a8882fd2674e532216b1a7518d2d/NipsEngine/Source/Engine/Render/Resource/Shader.h)

### 2. UberLit·UberUnlit 전환과 머티리얼의 표현 분리

메시의 공통 표면 처리 코드를 `UberSurface`로 묶고, 조명 모델을 선택하는 UberLit과 Unlit 뷰를 위한 셰이더 경로를 구성했습니다. 머티리얼에는 조명 모델과 인스턴스의 override 정보를 두고, 렌더 패스가 필요한 셰이더를 선택해 바인딩하도록 연결했습니다. 표면 데이터 처리와 조명 모델·뷰 모드 선택을 나눠, 같은 메시·머티리얼을 서로 다른 표현으로 그리는 구조를 정리했습니다.

근거: [Uber 셰이더·머티리얼 전환](https://github.com/jskim-research/Jungle_Week7_Team4/commit/6917c4c4193266dfea74ed28ca02486e0fdbeb80) · [UberSurface.hlsli](https://github.com/jskim-research/Jungle_Week7_Team4/blob/6917c4c4193266dfea74ed28ca02486e0fdbeb80/NipsEngine/Shaders/UberSurface.hlsli) · [Material.h](https://github.com/jskim-research/Jungle_Week7_Team4/blob/6917c4c4193266dfea74ed28ca02486e0fdbeb80/NipsEngine/Source/Engine/Render/Resource/Material.h)

### 3. 씬 조명을 공유하는 데칼 오버레이

데칼을 UberLit의 데칼 도메인으로 통합하고, 씬 조명을 받아 표면에 합성되는 경로로 확장했습니다. Opaque·Decal 패스에서 사용하는 라이트 버퍼·타일별 라이트 목록 연결을 `SceneLightBinding`에 모으고, 데칼 상수를 머티리얼 바인딩으로 전달했습니다. 패스 종료 시 공용 리소스의 바인딩을 해제하도록 구성해, 조명 반응을 추가하면서도 패스 간 리소스 상태를 구분했습니다.

근거: [조명 반응형 데칼 통합](https://github.com/jskim-research/Jungle_Week7_Team4/commit/ee54cc04667ad96faf72fbc33ac3eeef582747af) · [SceneLightBinding.h](https://github.com/jskim-research/Jungle_Week7_Team4/blob/ee54cc04667ad96faf72fbc33ac3eeef582747af/NipsEngine/Source/Engine/Render/Renderer/RenderFlow/SceneLightBinding.h)

### 4. 씬의 조명·안개와 연결되는 하늘 렌더링

SkyAtmosphere 컴포넌트와 전용 SkyRenderPass를 추가해, 카메라 방향에 따른 하늘·태양 표현을 풀스크린 패스로 그리도록 구성했습니다. 방향광에서 태양 방향과 높이를 읽고 낮·석양·밤 상태를 계산하며, 설정에 따라 Ambient Light와 Height Fog에도 색·강도를 반영하도록 연결했습니다. 에디터에서 조절한 하늘 설정이 하늘 렌더링과 주변 환경 효과에 함께 전달되는 흐름을 구현한 작업입니다.

근거: [Sky pass·SkyAtmosphere 추가](https://github.com/jskim-research/Jungle_Week7_Team4/commit/2b80a9ab39bae7bb3dc8e681e0744bbf8389dd94) · [SkyAtmosphereComponent.h](https://github.com/jskim-research/Jungle_Week7_Team4/blob/2b80a9ab39bae7bb3dc8e681e0744bbf8389dd94/NipsEngine/Source/Engine/Component/SkyAtmosphereComponent.h) · [SkyRenderPass.cpp](https://github.com/jskim-research/Jungle_Week7_Team4/blob/2b80a9ab39bae7bb3dc8e681e0744bbf8389dd94/NipsEngine/Source/Engine/Render/Renderer/RenderFlow/SkyRenderPass.cpp)

관련 PR: [셰이더 리플렉션 바인딩 PR](https://github.com/jskim-research/Jungle_Week7_Team4/pull/2)

## 문서와 실행 자료

- [원본 README](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/README.md)
- [Visual Studio 솔루션 · NipsEngine.sln](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/NipsEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/ReleaseBuild.bat)

원본 README에는 이전 주차의 제목·구성 설명이 남아 있습니다. 이 목차의 주차별 주제와 개인 기여는 해당 저장소의 커밋 이력을 함께 확인해 정리했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
