[전체 목차](../README.md) · [← 3주차](../week03/README.md) · [5주차 →](../week05/README.md)

# 4주차 · 메시·머티리얼과 ObjViewer

Jungle Engine 위에서 Editor, Client, ObjViewer를 함께 다루는 주차입니다. OBJ 모델의 불러오기·검수·내보내기와 에디터 렌더링 도구를 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/KraftonJungle3_Week4_Team6](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6) | 공개 | [cc564c2](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/tree/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- OBJ와 모델 에셋의 로드·변환
- Editor와 ObjViewer의 실행 흐름
- 선택 아웃라인과 렌더 리소스 관리

## 내 기여

모델을 불러와 검수하고 내보내는 ObjViewer와 선택 시각화, 자원 수명 관리 작업을 담당했습니다. 아래 설명은 `DDing-Ho` 작성 커밋의 실제 변경 내용을 기준으로 정리한 개인 작업입니다.

### OBJ import 옵션과 모델 검수 도구 확장

Forward·Up 축과 기존 변환 방식의 사용 여부를 `FObjLoadOptions`로 전달하도록 OBJ 로더를 확장했습니다. ObjViewer에는 와이어프레임, 정점·면 노말 표시와 길이 조절, 그리드 크기·두께 설정을 추가했습니다. 좌표계 설정과 노말 상태를 뷰어에서 확인할 수 있도록 import 처리와 검수 UI를 함께 연결했습니다.

근거: [ObjViewer import·디버그 뷰 개선 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/aa8e9b01ba73758f7aef12ba3a455a84333ce386) · [ObjManager.h](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/aa8e9b01ba73758f7aef12ba3a455a84333ce386/Engine/Source/Asset/ObjManager.h) · [ObjViewerDetailsWindow.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/aa8e9b01ba73758f7aef12ba3a455a84333ce386/ObjViewer/Source/ObjViewerDetailsWindow.cpp)

### 미리보기의 스케일을 모델 내보내기에 반영

모델을 내보낼 때 import 회전만 반영하던 베이킹 경로에 균일 스케일을 전달하도록 수정했습니다. 정점 위치에 스케일과 회전을 적용하고 노말에는 회전을 적용해, import 옵션에서 선택한 크기가 내보낸 메시 데이터에도 반영되도록 했습니다. 도구에서 확인한 변환과 저장되는 결과 사이의 차이를 수정한 작업입니다.

근거: [모델 스케일 베이킹 수정 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/f03ca1b4bf8eda476617bf1b1b503cbee1cb58f3) · [ObjViewerEngine.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/f03ca1b4bf8eda476617bf1b1b503cbee1cb58f3/ObjViewer/Source/ObjViewerEngine.cpp)

### 선택 마스크와 후처리 기반의 아웃라인

선택한 메시의 마스크와 스텐실 상태를 생성하고, 마스크에 Sobel 필터를 적용해 윤곽선을 합성하는 렌더링 경로를 구현했습니다. 화면 크기에 맞는 마스크 텍스처와 관련 RTV·SRV를 관리하고, 아웃라인 색·두께·임계값을 후처리 상수로 전달하도록 구성했습니다. 여러 선택 메시를 수집해 처리하는 인터페이스와 UI 연결도 함께 변경했습니다.

근거: [후처리 아웃라인 구현 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/bd91af38052d6345794c73b87e7e2cda7ebe3fae) · [Renderer.h](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/bd91af38052d6345794c73b87e7e2cda7ebe3fae/Engine/Source/Renderer/Renderer.h) · [OutlineSobelPixelShader.hlsl](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/bd91af38052d6345794c73b87e7e2cda7ebe3fae/Engine/Shaders/OutlineSobelPixelShader.hlsl)

### 메시 에셋 생성·캐시 해제의 수명주기 수정

OBJ·모델 로딩에서 `new`로 생성하던 `UStaticMesh`를 `FObjectFactory`를 통해 생성하도록 바꿨습니다. 엔진 종료 시에는 OBJ 캐시를 먼저 비우고, 이후 오브젝트 매니저의 제거 대상을 정리하도록 해제 순서를 보완했습니다. 메시가 엔진의 객체 관리 흐름에 들어오도록 맞춰, 자원 누수 문제를 생성 경로와 종료 경로 양쪽에서 다뤘습니다.

근거: [메시 자원 수명 관리 수정 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/eafe5d553a7ee9d27e3d9eb4cb4730636f84033d) · [ObjManager.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/eafe5d553a7ee9d27e3d9eb4cb4730636f84033d/Engine/Source/Asset/ObjManager.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/README.md)
- [Visual Studio 솔루션 · KraftonJungleEngine.sln](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/KraftonJungleEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/ReleaseBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
