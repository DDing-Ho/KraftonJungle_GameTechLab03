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

애니메이션을 에셋으로 편집·저장하고 캐릭터에 적용하는 흐름과, 지형에 맞게 포즈를 보정하는 IK 작업을 구현했습니다. 아래 내용은 `DDing-Ho` 작성 커밋으로 확인되는 범위이며, 팀의 스켈레탈 애니메이션 기능 전체와 구분합니다.

### 1. 저장 가능한 애니메이션 상태 머신과 그래프 에디터

`AnimInstanceAsset`을 추가해 Skeleton과 연결된 Blend Graph·State Machine 데이터를 저장할 수 있도록 했습니다. Sequence Player·Blend2·Output 노드, Float/Bool 파라미터와 전환 조건을 평가하는 런타임을 구성하고, Content Browser의 생성·열기 흐름을 그래프 에디터에 연결했습니다. 에디터에서는 State 내부 그래프와 경로 탐색, 호환 애니메이션 선택, 유효성 검사 결과 표시와 저장 차단을 제공해 잘못 연결된 그래프를 저장하기 전에 확인할 수 있게 했습니다.

근거: [상태 머신 에디터 커밋](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/c4381cb69d574eddb8c98ac5f55469206fc2cbfb) · [AnimGraphInstance.cpp](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/c4381cb69d574eddb8c98ac5f55469206fc2cbfb/KraftonEngine/Source/Engine/Animation/AnimGraphInstance.cpp)

### 2. Skeleton 호환성 검사와 Notify 저장·복원

SkeletalMeshComponent가 AnimInstanceAsset을 soft reference로 보관하고 로드 시 다시 적용하도록 연결했습니다. Details의 선택·드롭 후보는 같은 Skeleton을 사용하는 에셋으로 제한하고, AnimSequence 저장 시 기존 import metadata를 유지하면서 Notify 클래스와 편집 가능한 속성을 함께 기록했습니다. 기존 데이터 뒤에 선택적으로 Notify 정보를 추가하는 형식을 사용하고, 구형 에셋을 읽을 때는 Notify 데이터를 읽을 수 있는 남은 바이트 수를 검사하도록 했습니다.

근거: [에셋 연결·Notify 저장 커밋](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/33668ece0b8caef703f05c59ed33ddd9a813eb43) · [AnimDataModel.cpp](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/33668ece0b8caef703f05c59ed33ddd9a813eb43/KraftonEngine/Source/Engine/Animation/AnimDataModel.cpp)

### 3. Two-Bone IK 계산과 편집 UI의 연결

AnimationRuntime에 포즈의 전역 행렬 변환과 Two-Bone IK 계산을 추가하고, 애니메이션 포즈 평가 뒤 체인별 IK를 적용하도록 SkeletalMeshComponent에 연결했습니다. 에디터에서는 Root·Mid·End 본을 숫자 대신 본 목록에서 선택하게 하고, 부모·자식 관계에 맞는 후보만 보여주도록 필터링했습니다. 월드 좌표의 목표점을 컴포넌트 로컬 좌표로 변환하는 API와 체인 저장·활성화 설정까지 제공해 런타임 계산을 편집·제어 가능한 기능으로 만들었습니다.

근거: [IK 런타임·본 선택 커밋](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/6ebf0cca17bd07a6ee96e512ad66ee609ef1a768) · [AnimationRuntime.cpp](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/6ebf0cca17bd07a6ee96e512ad66ee609ef1a768/KraftonEngine/Source/Engine/Animation/AnimationRuntime.cpp)

### 4. 지면 탐색에 기반한 발 IK와 계단 이동 보정

고정 높이의 임시 바닥 판정을 지면 raycast 기반으로 바꾸고, 허용 가능한 계단 높이·하강 높이와 착지 처리를 추가했습니다. Lua의 FootIK는 보정 전 발 위치에서 지면을 탐색하고 목표 높이를 보간하며, 발의 접지 진입·이탈 기준을 나눠 이동 중 보정의 켜짐·꺼짐을 제어합니다. 과도한 높이 보정이나 공중 상태에서는 IK를 비활성화해, 지형 이동과 애니메이션 보정이 서로 다른 조건을 처리하도록 구성했습니다.

근거: [발 IK·계단 보정 커밋](https://github.com/keonwookang0914/Jungle_Week11_Team4/commit/5b3838e1bc0d9c6d4bbc873fd59c612864833403) · [FootIK.lua](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/5b3838e1bc0d9c6d4bbc873fd59c612864833403/KraftonEngine/Asset/Script/FootIK.lua)

## 문서와 실행 자료

- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/keonwookang0914/Jungle_Week11_Team4/blob/aba046b5bdecd4d5ec4dec40f05cb0cc92f899cb/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
