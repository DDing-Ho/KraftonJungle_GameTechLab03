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

HZB 기반 가시성 처리와 공간 자료구조의 갱신, 기즈모 피킹 작업을 담당했습니다. 아래 설명은 `DDing-Ho` 작성 커밋의 실제 변경 내용을 기준으로 정리한 개인 작업입니다.

### 클러스터 단위의 비동기 HZB 가시성 처리

가시성 후보를 개별 Primitive에서 공간적으로 묶은 Cluster 단위로 처리하고, 보이는 클러스터를 실제 렌더 대상 Primitive로 확장하는 흐름으로 변경했습니다. GPU 완료 쿼리와 결과 readback 상태를 관리하고, HZB 생성·컬링 GPU 시간과 readback 대기 지연·CPU 복사 시간을 분리해 기록하도록 구성했습니다. 컬링 결과뿐 아니라 각 처리 단계의 비용을 구분해 관찰할 수 있도록 렌더러·가시성 시스템·통계 출력을 함께 수정했습니다.

근거: [비동기 클러스터 HZB 컬링 커밋](https://github.com/DDing-Ho/W05_Team8/commit/ed34896d6f5b7bd7125a635f10421b1fc0d13569) · [VisibilitySystem.h](https://github.com/DDing-Ho/W05_Team8/blob/ed34896d6f5b7bd7125a635f10421b1fc0d13569/PerformanceEngine/Source/Visibility/VisibilitySystem.h) · [SceneRenderer.cpp](https://github.com/DDing-Ho/W05_Team8/blob/ed34896d6f5b7bd7125a635f10421b1fc0d13569/PerformanceEngine/Source/Renderer/SceneRenderer.cpp)

### 실시간 World BVH와 가시성 스냅샷의 정합성 관리

실시간으로 갱신되는 World BVH 위에 정적 가시성 클러스터를 파생 스냅샷으로 관리하도록 구조를 나눴습니다. BVH revision과 클러스터 revision, dirty 상태를 추적하고, 조회 시 필요한 스냅샷을 구성하거나 변경된 상태를 무효화하도록 처리했습니다. 동적 Primitive 표시와 스냅샷 유효성 검사를 연결해, 변경된 BVH에 오래된 노드 정보를 그대로 적용하는 문제를 다뤘습니다.

근거: [가시성 스냅샷 분리 커밋](https://github.com/DDing-Ho/W05_Team8/commit/3ae821fefd2202a5853fc0370ed2b1a1633a6b26) · [Scene.cpp](https://github.com/DDing-Ho/W05_Team8/blob/3ae821fefd2202a5853fc0370ed2b1a1633a6b26/PerformanceEngine/Source/Scene/Scene.cpp)

### 메시 캐시와 로컬 BVH를 사용하는 Transform 기즈모

이동·회전·스케일 핸들의 메시, GPU 버퍼와 로컬 BVH를 캐시 항목으로 묶고, 같은 키의 핸들을 다시 요청할 때 재사용하도록 구현했습니다. 피킹에서는 월드 레이를 핸들의 로컬 좌표로 변환한 뒤 로컬 BVH와 교차 검사해 선택할 축·평면을 구합니다. 핸들 생성·렌더링·교차 검사를 나누면서 World·Local 좌표계의 드래그 조작까지 연결해, 최적화 과제에서도 씬을 직접 편집할 도구를 구성했습니다.

근거: [캐시·로컬 BVH 기즈모 구현 커밋](https://github.com/DDing-Ho/W05_Team8/commit/be8ca18cb9d53edb7db20f8d32dfc2f3b384aed7) · [Gizmo.h](https://github.com/DDing-Ho/W05_Team8/blob/be8ca18cb9d53edb7db20f8d32dfc2f3b384aed7/PerformanceEngine/Source/GIzmo/Gizmo.h) · [Gizmo.cpp](https://github.com/DDing-Ho/W05_Team8/blob/be8ca18cb9d53edb7db20f8d32dfc2f3b384aed7/PerformanceEngine/Source/GIzmo/Gizmo.cpp)

## 문서와 실행 자료

- [과제·학습 문서](https://github.com/DDing-Ho/W05_Team8/blob/85301116e1574100962866580593088ecda1a29e/Docs/README.md)
- [오클루전 컬링 문서](https://github.com/DDing-Ho/W05_Team8/blob/85301116e1574100962866580593088ecda1a29e/Docs/OcclusionCulling.md)
- [Visual Studio 솔루션 · PerformanceEngine.sln](https://github.com/DDing-Ho/W05_Team8/blob/85301116e1574100962866580593088ecda1a29e/PerformanceEngine.sln)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
