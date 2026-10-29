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

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- IAssetLoader와 에셋 로딩·캐시 추가 — [0034a45](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/0034a457316853fa32082a6fe3dc6a44657083a0)
- Panel 인터페이스와 매니저 추가 — [52f666c](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/52f666c3cb61d997a011b8df6d21c2ab24fe25a2)
- Content Browser와 콘텐츠 인덱스 구현 — [77b0046](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/77b00462214feb23db39ce4fda43d47e58ac2780)
- Content Browser 드래그 앤 드롭 구현 — [643f51c](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/commit/643f51c9493c9df6b1b29854c9a7ef2132a14629)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/a587fc19e11341b3ee1509e7d3a408ded82f8f7e/README.md)
- [Visual Studio 솔루션 · Kraftonjungle_Team2.sln](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/a587fc19e11341b3ee1509e7d3a408ded82f8f7e/Kraftonjungle_Team2.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2/blob/a587fc19e11341b3ee1509e7d3a408ded82f8f7e/GenerateProjectFiles.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
