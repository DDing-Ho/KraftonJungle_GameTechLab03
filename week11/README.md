[전체 목차](../README.md) · [← 10주차](../week10/README.md) · [12주차 →](../week12/README.md)

# 11주차 · 스켈레탈 애니메이션·IK

스켈레탈 메시와 애니메이션 에셋·편집 도구를 확장한 주차입니다. 애니메이션 상태 머신, Notify, Two-Bone IK와 발 IK 작업을 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [keonwookang0914/Jungle_Week11_Team4](https://github.com/keonwookang0914/Jungle_Week11_Team4) | 공개 | [aba046b](https://github.com/keonwookang0914/Jungle_Week11_Team4/tree/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- FBX 스켈레탈 메시와 스켈레톤 에셋
- AnimInstanceAsset 상태 머신과 Notify 저장
- Two-Bone IK와 계단의 발 높이 보정

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- AnimInstanceAsset State Machine 에디터 추가 — [c4381cb](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/c4381cb69d574eddb8c98ac5f55469206fc2cbfb)
- AnimInstanceAsset 연결과 Notify 저장 추가 — [33668ec](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/33668ece0b8caef703f05c59ed33ddd9a813eb43)
- Two-Bone IK 런타임과 본 선택 UI 추가 — [6ebf0cc](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/6ebf0cca17bd07a6ee96e512ad66ee609ef1a768)
- 발 IK와 계단 단차 보정 구현 — [5b3838e](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/5b3838e1bc0d9c6d4bbc873fd59c612864833403)

## 문서와 실행 자료

- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
