# KraftonJungle_GameTechLab03

**강명호 · [DDing-Ho](https://github.com/DDing-Ho)**

크래프톤 정글 **Game Tech Lab 3기 · 게임 엔진·그래픽스 개발 포트폴리오**

**1~14주차와 5+주차 · 주차별 문서 15개 · 원본 저장소 17개**

DirectX 게임 제작에서 출발해 자체 3D 엔진과 에디터를 확장하고, 렌더링·애니메이션·파티클·물리 기능을 게임 제작으로 연결한 기록입니다. 각 주차에는 **구현 목적 → 설계와 동작 → 해결한 문제**를 중심으로 개인 기여를 정리하고, 실제 변경을 확인할 수 있는 커밋 링크를 붙였습니다.

[14주차 정글무쌍](week14/README.md) · [팀 시연 영상](https://youtu.be/-prBOp3srOc) · [12주차 파티클](week12/README.md) · [13주차 물리·차량](week13/README.md)

## 주요 기여 한눈에 보기

| 분야 | 직접 구현·개선한 내용 | 상세 기록 |
| --- | --- | --- |
| 엔진 구조·편집 도구 | 씬 컨텍스트와 ViewportClient, 기즈모, 패널·Content Browser, OBJ 검수 도구를 연결해 실행과 편집 흐름을 확장 | [2주차](week02/README.md) · [3주차](week03/README.md) · [4주차](week04/README.md) · [5+주차](week05-plus/README.md) |
| 렌더링·최적화 | 비동기 HZB 가시성 처리, 높이 안개, 셰이더 리플렉션 기반 바인딩, UberLit 조명과 SpotLight·PSM 그림자 작업 | [5주차](week05/README.md) · [6주차](week06/README.md) · [7주차](week07/README.md) · [8주차](week08/README.md) |
| 콘텐츠·애니메이션 | FBX import와 바이너리 메시 에셋, 애니메이션 상태 머신 편집, Notify 저장과 Two-Bone·발 IK를 구현·개선 | [10주차](week10/README.md) · [11주차](week11/README.md) |
| 파티클·물리 | 파티클 인스턴싱과 SubUV·Ribbon 모듈, PhysX 차량 구조와 Lua 탱크 조작, 카메라·물리 통계 기능을 확장 | [12주차](week12/README.md) · [13주차](week13/README.md) |
| 게임플레이·연출 | 카메라 셰이크의 편집·재생, 게임 UI, 군중 이동 보정과 스포너 제어, 보스 조우·사망 연출과 아웃트로를 연결 | [9주차](week09/README.md) · [14주차](week14/README.md) |

팀 프로젝트의 전체 기능과 개인이 작성한 작업은 주차별 문서에서 구분했습니다. 아래 목차를 통해 과제의 맥락과 기여 근거를 함께 볼 수 있습니다.

## 주차별 목차

주차를 누르면 프로젝트 요약, 구체적인 구현·문제 해결 기록, 원본 문서와 참조 버전을 볼 수 있습니다. 원본 열의 이름은 저장소 소유자입니다. 🔒 표시는 비공개 원본입니다.

| 주차 | 학습·프로젝트 | 정리 주제 | 원본 |
| --- | --- | --- | --- |
| [1주차](week01/README.md) | 피카츄 배구 | DirectX 게임 제작 | [DDing-Ho](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5) 🔒 |
| [2주차](week02/README.md) | 3D 엔진·에디터의 기초 | 엔진 프레임워크·기즈모 | [DDing-Ho](https://github.com/DDing-Ho/Jungle3_Week2_Team1) |
| [3주차](week03/README.md) | CO-PASS Engine | 에셋·에디터 워크플로우 | [DDing-Ho](https://github.com/DDing-Ho/KraftonJungle3_Week3_Team2) |
| [4주차](week04/README.md) | 메시·머티리얼과 ObjViewer | 에셋 도구·렌더링 | [DDing-Ho](https://github.com/DDing-Ho/KraftonJungle3_Week4_Team6) |
| [5주차](week05/README.md) | PerformanceEngine | 렌더링·피킹 최적화 | [DDing-Ho](https://github.com/DDing-Ho/W05_Team8) 🔒 |
| [5+주차](week05-plus/README.md) | 5+주차 확장 작업 | 컴포넌트·PIE 편집 흐름 | [CaptainTangerine](https://github.com/CaptainTangerine/KraftonJungle3_Week5Plus_Team8) · [mathison0](https://github.com/mathison0/Jungle_Week5plus_Team8) 🔒 |
| [6주차](week06/README.md) | 데칼·높이 안개 | 화면 공간 효과 | [esc10946](https://github.com/esc10946/Jungle_Week6_Team6) |
| [7주차](week07/README.md) | 조명·셰이더 파이프라인 | 리플렉션·전방 조명 | [jskim-research](https://github.com/jskim-research/Jungle_Week7_Team4) |
| [8주차](week08/README.md) | 그림자 렌더링 | SpotLight·PSM | [DDing-Ho](https://github.com/DDing-Ho/Jungle_Week8_Team8) |
| [9주차](week09/README.md) | 게임플레이·에디터 도구 | 카메라 셰이크·콘텐츠 탐색 | [chodott](https://github.com/chodott/Jungle_Week9_Team2) |
| [10주차](week10/README.md) | FBX·메시 에셋 파이프라인 | FBX import·바이너리 에셋 | [kim-kihoon](https://github.com/kim-kihoon/Jungle_Week10_Team2) · [DDing-Ho](https://github.com/DDing-Ho/Jungle_Week10_Team2) |
| [11주차](week11/README.md) | 스켈레탈 애니메이션·IK | 애니메이션 편집·런타임 | [keonwookang0914](https://github.com/keonwookang0914/Jungle_Week11_Team4) |
| [12주차](week12/README.md) | 파티클 시스템 | Cascade 스타일 파티클 | [DDing-Ho](https://github.com/DDing-Ho/Jungle_Week12_Team8) |
| [13주차](week13/README.md) | 물리·차량·카메라 | PhysX 차량·DOF | [puter2712git](https://github.com/puter2712git/Jungle_Week13_Team3) |
| [14주차](week14/README.md) | 정글무쌍 게임잼 | 자체 엔진 기반 액션 게임 | [puter2712git](https://github.com/puter2712git/Jungle_Week14_Team2) |

## 기술별 바로가기

- **엔진·에디터**: [2주차 프레임워크](week02/README.md), [3주차 에셋·패널](week03/README.md), [4주차 ObjViewer](week04/README.md), [5+주차 컴포넌트·PIE](week05-plus/README.md)
- **렌더링**: [5주차 최적화](week05/README.md), [6주차 화면 효과](week06/README.md), [7주차 셰이더·조명](week07/README.md), [8주차 그림자](week08/README.md)
- **콘텐츠·애니메이션**: [9주차 게임플레이 도구](week09/README.md), [10주차 FBX](week10/README.md), [11주차 애니메이션·IK](week11/README.md)
- **시뮬레이션·게임 제작**: [12주차 파티클](week12/README.md), [13주차 물리·차량](week13/README.md), [1주차 피카츄 배구](week01/README.md), [14주차 정글무쌍](week14/README.md)

## 원본과 기여를 읽는 방법

- 이 저장소는 주차별 문서와 원본 링크를 모은 목차입니다. 원본 저장소의 코드·브랜치·커밋·이슈·PR·공개 범위는 그대로 유지합니다.
- 원본은 팀 공동 결과물입니다. 각 문서의 **내 기여**는 `DDing-Ho` 작성 커밋의 실제 변경을 바탕으로 작성하고, 기능·수정 근거를 연결했습니다.
- 주차별 제목은 원본 문서와 작업 이력을 요약한 정리 주제입니다.
- **5+주차**는 CaptainTangerine과 mathison0의 원본을 모두 연결했습니다.
- **10주차**는 후속 작업이 확인되는 kim-kihoon 팀 저장소와 DDing-Ho의 초기 작업 저장소를 함께 연결했습니다.
- 비공개 원본은 접근 권한이 필요합니다. 이 공개 목차에는 과제 코드·에셋을 복사하지 않았습니다.

## 기록 기준

**2026-10-29**에 원본 저장소의 기본 브랜치 `main`, README·구현 문서와 작성자 커밋의 변경 내용을 확인했습니다. 원본 링크와 별도로 고정된 커밋 링크를 제공해, 이 목차가 참조하는 버전을 확인할 수 있게 했습니다.

기본 브랜치에 포함된 작성자 커밋 중 대표 작업을 골라 연결했습니다. 전체 기여·모든 브랜치를 열거한 목록은 아닙니다. 원본별 버전 정보는 [sources.json](sources.json)에서도 볼 수 있습니다.
