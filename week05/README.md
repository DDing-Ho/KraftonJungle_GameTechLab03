[전체 목차](../README.md) · [← 4주차](../week04/README.md) · [5+주차 →](../week05-plus/README.md)

# 5주차 · PerformanceEngine

렌더링과 피킹 성능을 개선하는 팀 과제입니다. 공간 인덱스, 가시성 판정과 오클루전 컬링을 중심으로 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/W05_Team8](https://github.com/DDing-Ho/W05_Team8) | 비공개 | [8530111](https://github.com/DDing-Ho/W05_Team8/tree/85301116e1574100962866580593088ecda1a29e) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- FPS·프레임 시간과 피킹 시간 측정
- BVH를 활용한 공간 질의
- 비동기 HZB 기반 가시성 처리

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- 비동기 클러스터 HZB 컬링 적용 — [ed34896](https://github.com/DDing-Ho/W05_Team8/commit/ed34896d6f5b7bd7125a635f10421b1fc0d13569)
- 가시성 스냅샷과 실시간 World BVH 분리 — [3ae821f](https://github.com/DDing-Ho/W05_Team8/commit/3ae821fefd2202a5853fc0370ed2b1a1633a6b26)
- 로컬 BVH 피킹을 사용하는 기즈모 추가 — [be8ca18](https://github.com/DDing-Ho/W05_Team8/commit/be8ca18cb9d53edb7db20f8d32dfc2f3b384aed7)

## 문서와 실행 자료

- [과제·학습 문서](https://github.com/DDing-Ho/W05_Team8/blob/85301116e1574100962866580593088ecda1a29e/Docs/README.md)
- [오클루전 컬링 문서](https://github.com/DDing-Ho/W05_Team8/blob/85301116e1574100962866580593088ecda1a29e/Docs/OcclusionCulling.md)
- [Visual Studio 솔루션 · PerformanceEngine.sln](https://github.com/DDing-Ho/W05_Team8/blob/85301116e1574100962866580593088ecda1a29e/PerformanceEngine.sln)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
