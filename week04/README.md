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

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- ObjViewer import와 디버그 뷰 개선 — [aa8e9b0](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/aa8e9b01ba73758f7aef12ba3a455a84333ce386)
- 모델 내보내기에 스케일 반영 — [f03ca1b](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/f03ca1b4bf8eda476617bf1b1b503cbee1cb58f3)
- 스텐실 기반 후처리 아웃라인으로 정리 — [bd91af3](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/bd91af38052d6345794c73b87e7e2cda7ebe3fae)
- 그래픽 리소스 누수 수정 — [eafe5d5](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/commit/eafe5d553a7ee9d27e3d9eb4cb4730636f84033d)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/README.md)
- [Visual Studio 솔루션 · KraftonJungleEngine.sln](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/KraftonJungleEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6/blob/cc564c2c41005b46ad24c1e5ea04d63f54b3cad9/ReleaseBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
