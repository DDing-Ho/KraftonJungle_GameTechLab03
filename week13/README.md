[전체 목차](../README.md) · [← 12주차](../week12/README.md) · [14주차 →](../week14/README.md)

# 13주차 · 물리·차량·카메라

물리 시뮬레이션과 차량 제어, 카메라 기능을 확장한 주차입니다. PhysX 차량 구조, Lua를 통한 탱크 조작과 카메라 DOF·파일럿 기능을 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [puter2712git/Jungle_Week13_Team3](https://github.com/puter2712git/Jungle_Week13_Team3) | 공개 | [bfd7c08](https://github.com/puter2712git/Jungle_Week13_Team3/tree/bfd7c08951dcc78d2687c15f5d9c760dad5564da) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- PhysX 차량 구조와 탱크 컴포넌트
- Lua 조작·터렛 제어와 주포 반동
- DOF·뷰포트 파일럿과 물리 통계

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- PhysX 차량 구조 재구성 — [692892f](https://github.com/puter2712git/Jungle_Week13_Team3/commit/692892f3439d744ee39b28b5ae78a790482ade87)
- 탱크 차량 컴포넌트와 Lua 조작 추가 — [a946c7a](https://github.com/puter2712git/Jungle_Week13_Team3/commit/a946c7a58838463ec04ca692dd831273e622654a)
- 카메라 액터와 뷰포트 파일럿 기능 추가 — [c1f410d](https://github.com/puter2712git/Jungle_Week13_Team3/commit/c1f410db3a3f23e15b4edb3835caefd6e0cce6bc)
- 물리 통계 오버레이 추가 — [cd32a15](https://github.com/puter2712git/Jungle_Week13_Team3/commit/cd32a15eb054f264f4601858b491c1fbbd6b117e)

## 문서와 실행 자료

- [스키닝 수정 기록](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/Docs/SkeletalMeshSkinningFixNotes.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/puter2712git/Jungle_Week13_Team3/blob/bfd7c08951dcc78d2687c15f5d9c760dad5564da/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
