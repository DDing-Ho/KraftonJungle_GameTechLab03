[전체 목차](../README.md) · [← 7주차](../week07/README.md) · [9주차 →](../week09/README.md)

# 8주차 · 그림자 렌더링

NipsEngine의 그림자 렌더링을 확장한 주차입니다. 라이트 수집과 SpotLight 그림자, Directional Shadow 관련 작업을 확인할 수 있습니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/Jungle_Week8_Team8](https://github.com/DDing-Ho/Jungle_Week8_Team8) | 공개 | [df26cc9](https://github.com/DDing-Ho/Jungle_Week8_Team8/tree/df26cc90045251698b397f987599323dd2d38c79) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 그림자를 만드는 라이트의 수집
- SpotLight 그림자 렌더링
- PSM Directional Shadow와 GPU 선택 힌트

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- 그림자 캐스팅 라이트 수집 추가 — [00f6f5f](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/00f6f5fe754062adf980d29f5dc46f050573b566)
- SpotLight 그림자 렌더링 추가 — [eeffe84](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/eeffe849e8315f9251c5b88d0219db12678786b4)
- PSM Directional Shadow 추가 — [e377f40](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/e377f40c6333edf2aa79c2e5d54cff23dd4c72ee)
- 고성능 GPU 사용 힌트 추가 — [11554b8](https://github.com/DDing-Ho/Jungle_Week8_Team8/commit/11554b8f4ee53dc9cd914f1182d8c9ab977d40f3)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/README.md)
- [Visual Studio 솔루션 · NipsEngine.sln](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/NipsEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/Jungle_Week8_Team8/blob/df26cc90045251698b397f987599323dd2d38c79/ReleaseBuild.bat)

원본 README에는 이전 주차의 제목·구성 설명이 남아 있습니다. 이 목차의 주차별 주제와 개인 기여는 해당 저장소의 커밋 이력을 함께 확인해 정리했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
