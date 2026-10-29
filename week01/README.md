[전체 목차](../README.md) · [2주차 →](../week02/README.md)

# 1주차 · 피카츄 배구

DirectX 기반의 피카츄 배구 게임을 제작한 팀 프로젝트입니다. 2인 플레이와 AI 상대 플레이, 충돌 처리와 점수·사운드 시스템을 다룹니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/KraftonJungle3_Week1_Team5](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5) | 비공개 | [8e5ebb8](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/tree/8e5ebb8cb3e98170922b99f96c7e767c6bc21c83) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 키보드 입력과 스프라이트 애니메이션
- 공·캐릭터·지형의 충돌과 게임 진행
- 텍스처·사운드 리소스 관리

## 내 기여

텍스처·사운드 리소스 관리와 게임 상태에 따른 UI·배경 동작을 담당했습니다. 아래 설명은 `DDing-Ho` 작성 커밋의 실제 변경 내용을 기준으로 정리한 개인 작업입니다.

### 텍스처 캐시와 엔진 자원 관리 구조

텍스처의 생성·셰이더 바인딩·해제를 `UTexture2D`로 분리하고, `UResourceManager`에서 파일 경로를 키로 사용하는 캐시를 구현했습니다. 같은 경로를 다시 요청하면 기존 객체를 반환하고, 관리자가 `unique_ptr`로 소유하도록 구성했습니다. 렌더러·리소스 매니저·씬 매니저의 초기화와 해제는 `UEngine`에서 순서대로 처리해, 게임 앱이 개별 자원의 수명 관리를 직접 처리하던 책임을 나눴습니다.

근거: [리소스 구조 추가 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/commit/4db5f27747ebbabf91c9b4d1da765ecbf9f4adf4) · [UResourceManager.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/blob/4db5f27747ebbabf91c9b4d1da765ecbf9f4adf4/KraftonJungle3_Week1_Team5/UResourceManager.cpp)

### FMOD 사운드 재생과 실패·종료 경로 정리

BGM·반복음·효과음이 사용하는 재생 흐름을 `StartSound`로 모으고, 채널을 일시 정지 상태로 만든 뒤 반복 모드와 볼륨을 설정하고 재생하도록 정리했습니다. 고정 채널과 동적으로 반환하는 채널을 구분해 추적하고, 재생 실패·정지·전체 종료 시 채널 참조를 정리했습니다. 사운드 파일 로딩이나 FMOD 초기화가 실패하면 생성한 자원을 해제하도록 보완해, 정상 재생뿐 아니라 실패 이후의 상태도 관리했습니다.

근거: [SoundManager 개선 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/commit/d485bafd157577b3273ff049de0bb88d4ffe4f5c) · [USoundManager.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/blob/d485bafd157577b3273ff049de0bb88d4ffe4f5c/KraftonJungle3_Week1_Team5/USoundManager.cpp)

### 경기 상태와 연결한 종료 UI·배경 애니메이션

게임 종료 상태에서 결과 안내 이미지를 표시하고, 크기를 보간해 등장하는 UI 애니메이션을 추가했습니다. 득점 시에는 구름 애니메이션에도 감속된 시간을 적용하고, 경기 종료 후에는 구름이 계속 갱신되도록 별도 업데이트 경로를 두었습니다. 게임 오브젝트의 진행을 멈추는 처리와 배경·안내 UI의 갱신을 구분해, 상태 전환에서 발생하던 시각적 불일치를 수정했습니다.

근거: [종료 UI·애니메이션 수정 커밋](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/commit/ebbc4d0f88b6e69c9e301cd5faa28cc4aeac96ba) · [UMainGameScene.cpp](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/blob/ebbc4d0f88b6e69c9e301cd5faa28cc4aeac96ba/KraftonJungle3_Week1_Team5/UMainGameScene.cpp)

## 문서와 실행 자료

- [원본 README](https://github.com/DDing-Ho/KraftonJungle3_Week1_Team5/blob/8e5ebb8cb3e98170922b99f96c7e767c6bc21c83/README.md)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
