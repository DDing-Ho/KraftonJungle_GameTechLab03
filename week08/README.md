[전체 목차](../README.md) · [← 7주차](../week07/README.md) · [9주차 →](../week09/README.md)

# 8주차 · 그림자 렌더링

NipsEngine의 그림자 렌더링을 확장한 주차입니다. 라이트 수집과 SpotLight 그림자, Directional Shadow 관련 작업을 확인할 수 있습니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/Jungle_Week8_Team8](https://github.com/DDing-Ho/Jungle_Week8_Team8) | 공개 | [df26cc9](https://github.com/DDing-Ho/Jungle_Week8_Team8/tree/df26cc90045251698b397f987599323dd2d38c79) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 그림자를 만드는 라이트의 수집
- SpotLight 그림자 렌더링
- PSM Directional Shadow와 GPU 선택 힌트

## 내 기여

그림자를 만드는 라이트의 수집에서 깊이 맵 생성·조명 셰이더 적용까지 이어지는 경로를 담당했습니다. 아래 내용은 `DDing-Ho`가 작성한 커밋의 실제 변경을 기준으로 정리했습니다.

### 1. 그림자용 라이트 데이터와 변환 행렬 수집

일반 조명 데이터와 함께 그림자용 라이트·변환 행렬을 수집해 RenderBus로 전달하는 구조를 추가했습니다. SpotLight는 위치·방향·외부 원뿔 각도와 감쇠 반경에서 그림자 카메라의 뷰·투영 행렬을 만들고, 방향광은 카메라 프러스텀의 분할 구간을 사용하도록 구성했습니다. 라이트의 그림자 설정과 실제 shadow pass에서 사용할 데이터를 연결하는 수집 단계를 맡았습니다.

근거: [그림자 캐스팅 라이트 수집](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/00f6f5fe754062adf980d29f5dc46f050573b566) · [RenderCollector.cpp](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/00f6f5fe754062adf980d29f5dc46f050573b566/NipsEngine/Source/Engine/Render/Scene/RenderCollector.cpp)

### 2. SpotLight 깊이 패스와 조명 셰이더의 그림자 판정

SpotLight별 깊이 맵을 텍스처 배열에 렌더링하고, 각 라이트가 사용할 슬라이스와 행렬·bias를 조명 단계에 전달하는 경로를 구현했습니다. UberLit에서는 픽셀의 월드 위치를 라이트 공간으로 변환해 깊이를 비교하고, 주변 3×3 샘플의 가시성을 평균해 조명 기여에 반영했습니다. 수집한 라이트 정보가 깊이 맵 생성과 최종 표면 음영으로 이어지도록 ShadowPass와 공용 라이트 바인딩을 함께 확장했습니다.

근거: [SpotLight 그림자 렌더링](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/eeffe849e8315f9251c5b88d0219db12678786b4) · [ShadowPass.cpp](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/eeffe849e8315f9251c5b88d0219db12678786b4/NipsEngine/Source/Engine/Render/Renderer/RenderFlow/ShadowPass.cpp) · [UberLit.hlsl](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/eeffe849e8315f9251c5b88d0219db12678786b4/NipsEngine/Shaders/UberLit.hlsl)

### 3. 방향광의 PSM 경로와 모드 선택

방향광의 그림자 모드를 CSM·PSM으로 구분하고, PSM에 필요한 카메라 변환과 post-projective 공간의 뷰·투영 행렬 계산 경로를 추가했습니다. 모드별 계산 결과를 공통 그림자 상수로 묶어 전달하고, 셰이더에서도 선택한 방식에 맞게 그림자를 판정하도록 연결했습니다. 기존 CSM 경로를 유지하면서 방향광의 그림자 방식을 선택할 수 있도록 구성한 작업입니다.

근거: [PSM Directional Shadow 추가](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/e377f40c6333edf2aa79c2e5d54cff23dd4c72ee) · [DirectionalLightComponent.h](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/e377f40c6333edf2aa79c2e5d54cff23dd4c72ee/NipsEngine/Source/Engine/Component/Light/DirectionalLightComponent.h) · [RenderCollector.cpp](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/e377f40c6333edf2aa79c2e5d54cff23dd4c72ee/NipsEngine/Source/Engine/Render/Scene/RenderCollector.cpp)

### 4. 하이브리드 GPU 환경의 실행 설정 보완

실행 파일에 NVIDIA Optimus와 AMD PowerXpress의 고성능 GPU 사용 요청 심볼을 내보내도록 추가했습니다. 프로젝트 빌드에 해당 소스를 포함해, 하이브리드 GPU 환경에서 실행 파일이 고성능 GPU를 선호한다는 힌트를 제공하도록 구성했습니다.

근거: [고성능 GPU 사용 힌트](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/11554b8f4ee53dc9cd914f1182d8c9ab977d40f3) · [HighPerformanceGpuHint.cpp](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/11554b8f4ee53dc9cd914f1182d8c9ab977d40f3/NipsEngine/HighPerformanceGpuHint.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/README.md)
- [Visual Studio 솔루션 · NipsEngine.sln](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/NipsEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/ReleaseBuild.bat)

원본 README에는 이전 주차의 제목·구성 설명이 남아 있습니다. 이 목차의 주차별 주제와 개인 기여는 해당 저장소의 커밋 이력을 함께 확인해 정리했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
