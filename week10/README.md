[전체 목차](../README.md) · [← 9주차](../week09/README.md) · [11주차 →](../week11/README.md)

# 10주차 · FBX·메시 에셋 파이프라인

FBX 데이터를 엔진의 메시·머티리얼 에셋으로 변환하고, 에디터에서 가져온 에셋을 런타임에서 사용하는 파이프라인을 확장한 주차입니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [kim-kihoon/Jungle_Week10_Team2](https://github.com/kim-kihoon/Jungle_Week10_Team2) | 공개 | [af7c585](https://github.com/kim-kihoon/Jungle_Week10_Team2/tree/af7c585f0b58eb404a86b6c6d24558dfb091f7f6) |
| [DDing-Ho-Archive/Jungle_Week10_Team2](https://github.com/DDing-Ho-Archive/Jungle_Week10_Team2) | 공개 | [e30f093](https://github.com/DDing-Ho-Archive/Jungle_Week10_Team2/tree/e30f09348923a36193a867310f239fc3ef30aabb) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- FBX SDK 연결과 importer 구조 정리
- 메시의 바이너리 에셋 처리
- Content Browser와 에디터 하단 드로어

## 내 기여

에셋을 가져오는 에디터 단계와 실제 게임에서 사용하는 런타임 단계를 분리하고, FBX 데이터를 엔진의 메시·머티리얼 에셋으로 연결하는 작업을 구현했습니다. 아래 내용은 `DDing-Ho` 작성 커밋의 변경 사항을 기준으로 정리한 개인 기여입니다.

### 1. FBX importer의 책임과 진입점 정리

정적 메시와 스켈레탈 메시 importer에 나뉘어 있던 공통 처리를 재구성했습니다. `FbxSceneDocument`에 SDK 로드·축/단위 변환·삼각형화를 모으고, `FbxSceneInspector`의 판별 결과를 메시·스켈레톤·머티리얼 전용 extractor가 사용하도록 분리했습니다. ResourceManager는 정적 메시 import를 먼저 시도하고 실패하면 다른 importer로 넘어가는 방식에서 `FFbxAssetImporter` 단일 진입점을 사용하는 방식으로 바꿔, 파일 판별과 데이터 추출의 경계를 명확히 했습니다.

근거: [책임 분리 커밋](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/80009184439707945cfb649ba4e684be1a92666d) · [FbxAssetImporter.cpp](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/80009184439707945cfb649ba4e684be1a92666d/NipsEngine/Source/Editor/Importer/Fbx/FbxAssetImporter.cpp)

### 2. 속성 경계를 보존하는 FBX 정점 중복 제거

삼각형마다 정점을 새로 추가하던 경로에 정점 키와 해시 맵을 도입해 같은 정점의 인덱스를 재사용하도록 했습니다. 위치뿐 아니라 노말·UV·색상을 비교하고, 스켈레탈 메시에서는 본 인덱스와 가중치까지 포함해 UV 경계나 스키닝 정보가 다른 정점이 잘못 합쳐지지 않도록 했습니다. 공유 정점의 탄젠트·비탄젠트는 누적한 뒤 정규화하여, 정점 재사용과 표면의 방향 정보 계산을 함께 처리했습니다.

근거: [중복 정점 처리 커밋](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/e0ae0ea891d016fc3c7ec9348bea5d0650c6264d) · [FbxStaticMeshExtractor.cpp](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/e0ae0ea891d016fc3c7ec9348bea5d0650c6264d/NipsEngine/Source/Editor/Importer/Fbx/FbxStaticMeshExtractor.cpp)

### 3. 원본 파일과 런타임 에셋의 분리·마이그레이션

OBJ·MTL 파싱을 에디터 importer로 이동하고, 런타임은 BIN 메시와 MAT/MATINST 머티리얼을 등록하도록 변경했습니다. 바이너리 헤더에는 원본 파일의 수정 시각과 해시를 저장하고, 머티리얼 슬롯에는 에셋 경로를 남겨 컴파일된 메시에서 기본 재질을 복원할 수 있게 했습니다. 기존 Scene 참조를 새 에셋 경로로 옮기면서 구형 키의 호환 처리는 유지하고, 기존 머티리얼을 자동 생성 과정에서 덮어쓰지 않도록 처리했습니다.

근거: [바이너리 에셋 전환 커밋](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/6bb16414647994d25abba64e4cfd64c84ce072e4) · [ObjStaticMeshImporter.cpp](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/6bb16414647994d25abba64e4cfd64c84ce072e4/NipsEngine/Source/Editor/Importer/ObjStaticMeshImporter.cpp)

### 4. 콘텐츠 탐색에서 월드 배치까지 이어지는 드로어

에디터 하단에 콘텐츠 드로어를 추가해 폴더 트리·에셋 그리드·검색·종류별 필터를 제공했습니다. 에셋 목록을 보는 기능과 함께 메시를 월드에 배치하는 경로를 연결하고, 창 높이 조절과 열림 상태·애니메이션을 관리하도록 구성했습니다. 에셋 파이프라인의 결과물을 편집 화면에서 찾아 사용하는 흐름까지 구현한 작업입니다.

근거: [콘텐츠 드로어 커밋](https://github.com/kim-kihoon/Jungle_Week10_Team2/commit/4634e3df7d524503169f491a6d89cfae846ab1e9) · [EditorContentDrawerWidget.cpp](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/4634e3df7d524503169f491a6d89cfae846ab1e9/NipsEngine/Source/Editor/UI/EditorContentDrawerWidget.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/README.md)
- [Visual Studio 솔루션 · NipsEngine.sln](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/NipsEngine.sln)
- [SetupDependencies.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/SetupDependencies.bat)
- [GenerateProjectFiles.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/GenerateProjectFiles.bat)
- [BuildEditorRelease.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/BuildEditorRelease.bat)
- [ReleaseBuild.bat](https://github.com/kim-kihoon/Jungle_Week10_Team2/blob/af7c585f0b58eb404a86b6c6d24558dfb091f7f6/ReleaseBuild.bat)

kim-kihoon 저장소에는 2026-05-13의 작성자 커밋이 확인됩니다. DDing-Ho-Archive로 이전한 저장소에는 2026-05-08까지의 초기 FBX 작업이 남아 있어 두 원본을 모두 연결했습니다.

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
