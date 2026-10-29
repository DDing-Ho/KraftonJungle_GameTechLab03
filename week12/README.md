[전체 목차](../README.md) · [← 11주차](../week11/README.md) · [13주차 →](../week13/README.md)

# 12주차 · 파티클 시스템

Cascade 스타일의 파티클 런타임과 에디터를 확장한 주차입니다. 스프라이트·메시 렌더링, SubUV, Ribbon, Spawn Per Unit과 수명에 따른 색상 변화 작업을 정리합니다.

## 원본 저장소

| 저장소 | 공개 범위 | 참조 버전 |
| --- | --- | --- |
| [DDing-Ho/Jungle_Week12_Team8](https://github.com/DDing-Ho/Jungle_Week12_Team8) | 공개 | [394e0fd](https://github.com/DDing-Ho/Jungle_Week12_Team8/tree/394e0fd69076814e5eb1481feafecc48276fb88d) |

참조 버전은 2026-10-29에 확인한 원본 `main` 브랜치의 커밋입니다. 비공개 원본은 접근 권한이 있는 계정으로 열 수 있습니다.

## 핵심 내용

- 파티클 모듈과 인스턴싱 렌더링
- SubUV·Ribbon·Spawn Per Unit
- 머티리얼 선택·편집과 구현 상태 검토 문서

## 내 기여

파티클 런타임의 데이터를 실제 D3D11 렌더링으로 연결하고, 이펙트 제작자가 에디터에서 설정·저장할 수 있는 모듈을 구현했습니다. 아래 내용은 `DDing-Ho` 작성 커밋의 렌더링·모듈·직렬화 변경을 기준으로 정리했습니다.

### 1. 공용 quad와 인스턴스 버퍼를 이용한 스프라이트 렌더링

파티클별 정점·인덱스를 CPU에서 확장하는 대신 공용 quad와 위치·회전·크기·색상 인스턴스 데이터를 사용하는 D3D11 인스턴싱 경로를 구성했습니다. Draw command에 instance buffer·stride·count를 전달하고, 셰이더 리플렉션의 input layout도 정점 슬롯과 per-instance 슬롯을 구분하게 확장했습니다. emitter·material별 구간은 FirstInstance와 InstanceCount로 나눠, 기존 일반 메시 draw 경로와 파티클 인스턴싱 경로가 함께 동작하도록 했습니다.

근거: [인스턴싱 구현 커밋](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/c61bd7b7e019be46e2c954301546dfa94e94dc95) · [ParticleSceneProxy.cpp](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/c61bd7b7e019be46e2c954301546dfa94e94dc95/KraftonEngine/Source/Engine/Render/Proxy/ParticleSceneProxy.cpp)

### 2. SubUV 프레임 계산부터 셰이더 보간까지 연결

SubImage Index와 SubUV Movie 모듈을 추가하고, 아틀라스의 행·열 수와 재생 방식에 따라 파티클의 프레임을 계산하도록 했습니다. 런타임에서 두 UV 영역과 보간 비율을 만들고 셰이더에서는 두 프레임의 샘플을 섞어 스프라이트 시트 애니메이션을 표현했습니다. 모듈 생성 메뉴·에셋 직렬화·파티클별 렌더 데이터까지 함께 갱신해, 편집한 설정이 저장·재생 경로로 이어지도록 구성했습니다.

근거: [SubUV 모듈 커밋](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/a73e0bf701b4225be4c645f522759064b19f46a8) · [ParticleSprite.hlsl](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/a73e0bf701b4225be4c645f522759064b19f46a8/KraftonEngine/Shaders/Particles/ParticleSprite.hlsl)

### 3. 소스 추적과 이동 거리 샘플링을 갖춘 Ribbon

Ribbon 전용 emitter instance와 vertex/index 데이터를 추가하고, 자신이 움직이는 궤적과 다른 source emitter를 따라가는 궤적을 모두 처리하도록 했습니다. SpawnId·SourceSpawnId를 이용해 소스별 trail을 분리하고 소스가 사라지는 경우를 처리했으며, Spawn Per Unit은 이동 거리에 따라 샘플을 생성하도록 연결했습니다. 전용 셰이더·동적 버퍼와 에디터 TypeData 전환 UI도 함께 구현해, 궤적 생성 정책에서 화면 출력까지 하나의 흐름으로 구성했습니다.

근거: [Ribbon·Spawn Per Unit 커밋](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/60bc0ffbc998ed0e2557ee3c3dc00d5de673cb36) · [ParticleEmitterInstance.cpp](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/60bc0ffbc998ed0e2557ee3c3dc00d5de673cb36/KraftonEngine/Source/Engine/Particles/Runtime/ParticleEmitterInstance.cpp)

### 4. 수명에 따른 색상·투명도 제어 모듈

Color Over Life 모듈이 파티클의 RelativeTime을 기준으로 RGB와 Alpha를 각각 평가하도록 구현했습니다. 생성 시 설정한 BaseColor는 유지하고 최종 렌더 색상만 갱신하며, 기존 Distribution·Curve 편집기를 재사용해 색상과 투명도 변화를 조정하도록 했습니다. 새 모듈을 에디터 메뉴와 저장·로드 팩토리에 등록해, 런타임 동작과 에셋 편집·저장을 연결했습니다.

근거: [Color Over Life 커밋](https://github.com/DDing-Ho/Jungle_Week12_Team8/commit/599ae8a3aac62b81dc55522726067e181d7aeac3) · [ParticleModules.cpp](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/599ae8a3aac62b81dc55522726067e181d7aeac3/KraftonEngine/Source/Engine/Particles/Modules/ParticleModules.cpp)

## 문서와 실행 자료

- [파티클 시스템 구현 상태 검토](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/Docs/CascadeParticleSystemImplementationReview.md)
- [Visual Studio 솔루션 · KraftonEngine.sln](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/KraftonEngine.sln)
- [GenerateProjectFiles.bat](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/GenerateProjectFiles.bat)
- [ReleaseBuild.bat](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/ReleaseBuild.bat)
- [GameBuild.bat](https://github.com/DDing-Ho/Jungle_Week12_Team8/blob/394e0fd69076814e5eb1481feafecc48276fb88d/GameBuild.bat)

빌드 환경과 의존성은 원본 문서·프로젝트 파일을 참고하세요. 이 목차 저장소에는 과제의 소스 코드나 실행 에셋을 복사하지 않았습니다.
