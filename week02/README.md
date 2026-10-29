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

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- SceneContext와 프리뷰 씬 도입 — [5ef09bd](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/5ef09bd3b1e77dd3fc049fcc2ff1f3caf560c95e)
- ViewportClient와 에디터 연결 — [ec46c6a](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/ec46c6ac19737dc4c6cecec1ad9b6a1873daa1ab)
- 기즈모 상호작용·렌더링과 문서 작성 — [a932162](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/a9321626603bf0d6967435b55b65606d9fec47c4)
- 직교 카메라와 피킹 개선 — [7dc690c](https://github.com/DDing-Ho/Jungle3_Week2_Team1/commit/7dc690cf0ff416596955a6c1b1be4ae1f75c9903)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/README.md)
- [Visual Studio 솔루션 · KraftonJungleEngine.sln](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/KraftonJungleEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/Jungle3_Week2_Team1/blob/7dc690cf0ff416596955a6c1b1be4ae1f75c9903/ReleaseBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
