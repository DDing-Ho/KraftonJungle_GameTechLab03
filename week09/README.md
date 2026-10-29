[전체 목차](../README.md) · [← 8주차](../week08/README.md) · [10주차 →](../week10/README.md)

# 9주차 · 게임플레이·에디터 도구

CrashEngine에서 게임플레이와 에디터 도구를 함께 확장한 주차입니다. 카메라 셰이크의 패턴·편집·재생과 게임 UI, 콘텐츠 탐색 흐름을 중심으로 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [chodott/Jungle_Week9_Team2](https://github.com/chodott/Jungle_Week9_Team2) | 공개 | [a5aeee8](https://github.com/chodott/Jungle_Week9_Team2/tree/a5aeee8d58b47a3efc69bb75541ad666a2f74990) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 패턴 기반 카메라 셰이크
- 시퀀스 카메라 셰이크 편집과 게임플레이 재생
- Output Log·Content Browser와 Lua 스크립트 탐색

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- 카메라 셰이크의 패턴 기반 구조 구현 — [2f6bbfd](https://github.com/chodott/Jungle_Week9_Team2/commit/2f6bbfd1b14a51724d7e7f30cbb3582f574b281b)
- 시퀀스 카메라 셰이크 에디터 구현 — [a8718f1](https://github.com/chodott/Jungle_Week9_Team2/commit/a8718f15352c63e519c34d66fc552eeec4940f39)
- 게임플레이 카메라 셰이크 재생 추가 — [e44be78](https://github.com/chodott/Jungle_Week9_Team2/commit/e44be78f34aec1ecbe255ca438f644a9a590ae27)
- 레벨업 선택창과 스코어보드 UI 개선 — [b3e819c](https://github.com/chodott/Jungle_Week9_Team2/commit/b3e819c0e4cefd864c00158d655457663003c7cc)

관련 PR: [에디터 드로어·Output Log·Lua 탐색 PR](https://github.com/chodott/Jungle_Week9_Team2/pull/1)

## 문서와 실행 자료

- [Visual Studio 솔루션 · CrashEngine.sln](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/CrashEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/GenerateProjectFiles.bat)
- [EditorBuild.bat](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/EditorBuild.bat)
- [GameBuild.bat](https://github.com/chodott/Jungle_Week9_Team2/blob/a5aeee8d58b47a3efc69bb75541ad666a2f74990/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
