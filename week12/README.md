[전체 목차](../README.md) · [← 11주차](../week11/README.md) · [13주차 →](../week13/README.md)

# 12주차 · 파티클 시스템

Cascade 스타일의 파티클 런타임과 에디터를 확장한 주차입니다. 스프라이트·메시 렌더링, SubUV, Ribbon, Spawn Per Unit과 수명에 따른 색상 변화 작업을 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/Jungle_Week12_Team8](https://github.com/DDing-Ho/Jungle_Week12_Team8) | 공개 | [394e0fd](https://github.com/DDing-Ho/Jungle_Week12_Team8/tree/394e0fd69076814e5eb1481feafecc48276fb88d) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 파티클 모듈과 인스턴싱 렌더링
- SubUV·Ribbon·Spawn Per Unit
- 머티리얼 선택·편집과 구현 상태 검토 문서

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- 스프라이트 파티클 인스턴싱 렌더링 구현 — [c61bd7b](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/c61bd7b7e019be46e2c954301546dfa94e94dc95)
- Cascade SubUV 모듈 구현 — [a73e0bf](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/a73e0bf701b4225be4c645f522759064b19f46a8)
- Ribbon과 Spawn Per Unit 구현 — [60bc0ff](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/60bc0ffbc998ed0e2557ee3c3dc00d5de673cb36)
- Color Over Life 모듈 추가 — [599ae8a](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/599ae8a3aac62b81dc55522726067e181d7aeac3)

## 문서와 실행 자료

- [파티클 시스템 구현 상태 검토](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/Docs/CascadeParticleSystemImplementationReview.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
