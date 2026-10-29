[전체 목차](../README.md) · [← 6주차](../week06/README.md) · [8주차 →](../week08/README.md)

# 7주차 · 조명·셰이더 파이프라인

NipsEngine의 셰이더 바인딩과 조명 경로를 확장한 주차입니다. 셰이더 리플렉션을 통한 파라미터 업로드, UberLit 기반 조명 처리와 하늘 렌더링을 중심으로 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [jskim-research/Jungle_Week7_Team4](https://github.com/jskim-research/Jungle_Week7_Team4) | 공개 | [b076888](https://github.com/jskim-research/Jungle_Week7_Team4/tree/b0768887dd289b005042df80afeacb7e2a0b7d63) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 셰이더 리플렉션 기반의 렌더 파라미터 연결
- 전방 조명과 UberLit 셰이더
- 조명 반응형 데칼과 SkyAtmosphere

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- 셰이더 리플렉션 기반 바인딩 시스템 도입 — [e7f10bc](https://github.com/jskim-research/Jungle_Week7_Team4/commit/e7f10bc3e738a8882fd2674e532216b1a7518d2d)
- UberLit 전환과 머티리얼·리소스 정리 — [6917c4c](https://github.com/jskim-research/Jungle_Week7_Team4/commit/6917c4c4193266dfea74ed28ca02486e0fdbeb80)
- 데칼을 조명 반응형 오버레이로 통합 — [ee54cc0](https://github.com/jskim-research/Jungle_Week7_Team4/commit/ee54cc04667ad96faf72fbc33ac3eeef582747af)
- Sky pass와 SkyAtmosphere 추가 — [2b80a9a](https://github.com/jskim-research/Jungle_Week7_Team4/commit/2b80a9ab39bae7bb3dc8e681e0744bbf8389dd94)

관련 PR: [셰이더 리플렉션 바인딩 PR](https://github.com/jskim-research/Jungle_Week7_Team4/pull/2)

## 문서와 실행 자료

- [원본 README](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/README.md)
- [Visual Studio 솔루션 · NipsEngine.sln](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/NipsEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/jskim-research/Jungle_Week7_Team4/blob/b0768887dd289b005042df80afeacb7e2a0b7d63/ReleaseBuild.bat)

원본 README에는 이전 주차의 제목·구성 설명이 남아 있습니다. 이 목차의 주차별 주제와 개인 기여는 해당 저장소의 커밋 이력을 함께 확인해 정리했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
