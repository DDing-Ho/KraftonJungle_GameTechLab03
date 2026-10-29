[전체 목차](../README.md) · [← 5+주차](../week05-plus/README.md) · [7주차 →](../week07/README.md)

# 6주차 · 데칼·높이 안개

깊이·노말 데이터를 활용하는 화면 효과와 충돌 기반 게임플레이를 확장한 주차입니다. 팀 구현 문서에는 Decal, Fireball, Exponential Height Fog와 관련 에디터 기능이 정리되어 있습니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [esc10946/Jungle_Week6_Team6](https://github.com/esc10946/Jungle_Week6_Team6) | 공개 | [4285aef](https://github.com/esc10946/Jungle_Week6_Team6/tree/4285aef390ae572bfa2433b92a039ee4ef13b397) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- Projection Decal과 충돌 지점의 데칼 생성
- 깊이 버퍼를 이용한 월드 위치 복원
- Exponential Height Fog와 효과 통계·표시 제어

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- 지수 높이 포그의 기본 렌더링 경로 추가 — [8bb9917](https://github.com/esc10946/Jungle_Week6_Team6/commit/8bb9917a421a65f1653c7c12efdaea6b585c5da5)
- Exponential Height Fog 구현 문서 작성 — [fa29bc6](https://github.com/esc10946/Jungle_Week6_Team6/commit/fa29bc6673182c7a2ae17e062156d0d5f0a4aae9)
- 버그 수정과 Decal Stat 조건 보완 — [4b5caf0](https://github.com/esc10946/Jungle_Week6_Team6/commit/4b5caf0ff7a95d0e79215669aaa8b15b0a651551)

## 문서와 실행 자료

- [팀 구현 요약](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/Docs/W06_Team6_%EC%9E%A5%EB%AF%BC%EC%A4%80%EA%B0%95%EB%AA%85%ED%98%B8%EA%B9%80%ED%98%B8%EC%A4%80%EC%A1%B0%ED%98%84%EC%84%9D.md)
- [높이 안개 구현 문서](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/Docs/exponential-height-fog.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/esc10946/Jungle_Week6_Team6/blob/4285aef390ae572bfa2433b92a039ee4ef13b397/ReleaseBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
