[전체 목차](../README.md) · [← 9주차](../week09/README.md) · [11주차 →](../week11/README.md)

# 10주차 · FBX·메시 에셋 파이프라인

FBX import와 메시 에셋 파이프라인을 확장한 주차입니다. 5월 13일까지의 작성자 커밋이 확인되는 kim-kihoon 팀 저장소를 우선 연결하고, DDing-Ho의 초기 작업 저장소도 함께 연결합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [kim-kihoon/Jungle_Week10_Team2](https://github.com/kim-kihoon/Jungle_Week10_Team2) | 공개 | [af7c585](https://github.com/kim-kihoon/Jungle_Week10_Team2/tree/af7c585f0b58eb404a86b6c6d24558dfb091f7f6) |
| [DDing-Ho/Jungle_Week10_Team2](https://github.com/DDing-Ho/Jungle_Week10_Team2) | 공개 | [e30f093](https://github.com/DDing-Ho/Jungle_Week10_Team2/tree/e30f09348923a36193a867310f239fc3ef30aabb) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- FBX SDK 연결과 importer 구조 정리
- 메시의 바이너리 에셋 처리
- Content Browser와 에디터 하단 드로어

## 내 기여

`DDing-Ho`가 작성한 기능·수정 커밋을 연결했습니다. 위의 핵심 내용은 팀 프로젝트의 범위이며, 아래 항목은 그중 작성자 이력으로 확인되는 작업입니다.

- FBX importer를 계층별로 분리 — [8000918](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/80009184439707945cfb649ba4e684be1a92666d)
- FBX 중복 정점 처리 추가 — [e0ae0ea](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/e0ae0ea891d016fc3c7ec9348bea5d0650c6264d)
- StaticMesh를 바이너리 에셋 기준으로 전환 — [6bb1641](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/6bb16414647994d25abba64e4cfd64c84ce072e4)
- 에디터 콘텐츠 드로어 추가 — [4634e3d](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/4634e3df7d524503169f491a6d89cfae846ab1e9)

## 문서와 실행 자료

- [원본 README](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/README.md)
- [Visual Studio 솔루션 · NipsEngine.sln](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/NipsEngine.sln)
- [SetupDependencies.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/SetupDependencies.bat)
- [GenerateProjectFiles.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/GenerateProjectFiles.bat)
- [BuildEditorRelease.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/BuildEditorRelease.bat)
- [ReleaseBuild.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/ReleaseBuild.bat)

kim-kihoon 저장소에는 2026-05-13의 작성자 커밋이 확인됩니다. DDing-Ho 저장소에는 2026-05-08까지의 초기 FBX 작업이 남아 있어 두 원본을 모두 연결했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
