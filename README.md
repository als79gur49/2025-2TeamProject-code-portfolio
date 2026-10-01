# Urban Tour — 코드 열람용 포트폴리오

팀 프로젝트의 프로그래밍 구조를 검토하기 위한 로컬 소스 사본입니다. 씬·프리팹·실제 데이터·외부 자산과 Unity meta 파일을 제외했으므로 실행 가능한 Unity 프로젝트가 아닙니다. 이 사본에 대해 빌드, 실행 또는 테스트 통과를 주장하지 않습니다.

## 기준과 범위

- 원본: [als79gur49/2025-2TeamProject](https://github.com/als79gur49/2025-2TeamProject)
- 선택 브랜치: `feature/carddata-refactoring`
- 고정 커밋: [8b1f53250f18e622b71ca302cfda816433d14852](https://github.com/als79gur49/2025-2TeamProject/commit/8b1f53250f18e622b71ca302cfda816433d14852)
- Git 관찰: 선택 커밋은 조회 시 main의 `f938b3502f829ad74d83936e4db52974267111cf`보다 158커밋 앞서고 0커밋 뒤처집니다. 조회된 `2025-10-17colleage`와 main의 head도 선택 커밋의 이력에 포함됩니다.
- 사용자 확인: 최신 기준을 선택했습니다. 공식 최종 제출본이라는 증거는 확인하지 않았습니다.
- 사용자 확인 개발기간: **2025년 9~12월**.
- Git 커밋 관찰기간(UTC): 2025-09-06 04:25:25 ~ 2025-12-12 17:46:12. 이는 Git author 날짜 범위이며 실제 개발의 정확한 시작·종료일이나 제출일을 증명하지 않습니다.

원본 트리 19,230개 파일 / C# 436개를 이번 작업에서 GitHub 트리로 다시 확인했습니다. 포함 범위는 `Assets/Script/` 아래 C# 409개, `Assets/Script/Game.Scripts.asmdef`, 문맥 3개로 총 413개입니다. 문맥 파일의 원본 경로는 MANIFEST.csv에 기록하고 `ReviewContext/Packages/`와 `ReviewContext/ProjectSettings/`로 배치했습니다. 보조 문서 5개를 더해 총 418개 파일입니다.

원본 경로와 소스 바이트를 보존했습니다. 소스의 깨진 주석(예: UIPanelController)을 수정하지 않았습니다. 원본 README는 오래된 Claude 설계 초안이므로 복사하지 않고 이 문서를 새로 작성했습니다.

## 코드 읽기 안내

| 검토 주제 | 근거 파일 |
| --- | --- |
| 마나 예산 안에서 휴리스틱 가치에 따른 0/1 배낭 카드 조합 선택 | [KnapsackCardSelector](Assets/Script/Game/AI/KnapsackCardSelector.cs), [EnemyAIController](Assets/Script/Game/AI/EnemyAIController.cs), [CardValueInfo](Assets/Script/Game/AI/CardValueInfo.cs) |
| 6단계 턴 흐름 | [TurnPhase](Assets/Script/Game/Services/TurnPhase.cs), [TurnService](Assets/Script/Game/Services/TurnService.cs) |
| 그리드 이동과 전투 | [GridController](Assets/Script/Game/Components/GridController.cs), [Unit](Assets/Script/Game/Unit.cs), [UnitService](Assets/Script/Game/Services/UnitService.cs) |
| 카드 효과 정의와 적용 | [Effects 폴더](Assets/Script/Game/Card/Effects/) |
| 판단과 실행 분리 | [IUnitAI](Assets/Script/Game/Interfaces/IUnitAI.cs), [BasicUnitAI](Assets/Script/Game/Components/BasicUnitAI.cs), [Unit](Assets/Script/Game/Unit.cs) |
| ServiceLocator와 수동 의존성 주입 | [ServiceLocator](Assets/Script/Game/Core/ServiceLocator.cs), [GameInitializer](Assets/Script/Game/Core/GameInitializer.cs), [CardServiceManager](Assets/Script/Game/Managers/CardServiceManager.cs) |

카드 선택은 평가된 정수 가치의 조합을 마나 제약 아래 최적화합니다. 가치와 위치 평가는 휴리스틱이며, 이후 실행 및 필드 상태 변경이 있으므로 전체 게임 전략의 전역 최적성이나 카드 간 시너지의 완전한 최적화를 의미하지 않습니다. 턴 단계는 TurnStart → EnemySummon → AllySummon → EnemyAction → AllyAction → TurnEnd입니다.

## 원본 환경 문맥

ProjectVersion.txt와 manifest/lock 근거: Unity 2022.3.62f1, URP 14.0.12, TextMeshPro 3.0.7, Cinemachine 2.10.5, Newtonsoft JSON 3.2.2, Test Framework 1.1.33. 이는 원본 의존성 문맥이며 사본에서 설치하거나 실행한 결과가 아닙니다.

DOTween/Pro API 참조는 자체 코드에서 유지했고 외부 코드·DLL은 포함하지 않았습니다. 정확한 설치 버전은 미확인입니다. 고정 원본의 DOTween.dll(blob `57112d34beef1b8bb4f78782d752c7bef2452e0c`, 175,616바이트)과 DOTweenPro.dll(blob `1c376027b5137fc6b36b3334cf4115922de9adb3`, 16,384바이트)을 읽으려 했으나 연결 도구가 바이너리를 UTF-8로 해석하다 실패했습니다. 따라서 DLL 메타데이터·내장 버전 문자열은 조사하지 못했습니다. 라이브러리를 실행하거나 인증 경로를 우회하지 않았습니다.

원본의 두 DLL `.meta`는 Unity PluginImporter 설정만 담고 설치 버전이 없었습니다. 플러그인 readme와 Pro C# 8개의 버전 관련 문구도 확인했습니다. readme의 1.2.000 / 1.0.000 및 Pro 소스의 옛 버전 숫자는 업그레이드·호환성 안내이므로 설치 버전으로 쓰지 않았습니다. 읽기 시도·문서 blob 근거는 VALIDATION.json의 dotween 항목에 기록했습니다.

## 정적 제약과 보존된 불일치

- asmdef가 `Unity.InputSystem`을 참조하지만 manifest와 packages-lock에 `com.unity.inputsystem`이 없습니다.
- UnityEditor import 및 에디터 코드가 포함되어 있고, GameInitializer에는 `PlasticPipe.PlasticProtocol.Messages`, ActionEvaluator에는 `Codice.Client.BaseCommands.Import.Commit` import가 있습니다. 외부/에디터 의존성이 남아 있습니다.
- TileOccupancyIntegrationTest가 현행 GameServiceManager에 없는 `Instance` / `GetService<T>()` 구 API를 참조합니다. 테스트 이름이나 과거 커밋 메시지는 현 시점 테스트 통과 증거가 아닙니다.
- GridController.CanMoveUnit은 메서드 시작에서 즉시 `true`를 반환해 뒤의 검증 로직에 도달하지 않습니다.
- UIPanelController의 깨진 주석을 비롯한 원본 텍스트와 기존 코드는 그대로 보존했습니다.

이 항목들은 정적 열람 결과입니다. 원본 수정이나 버그 수정을 수행하지 않았습니다.

## 제외와 검증

후보 밖 C# 27개를 제외했습니다: DOTween/Pro 16개, Layer Lab 2개, Unity TutorialInfo 2개, 루트 CardUIRefactored_Improved_Part1/2 2개, backup_carddata 3개, Assets/_ConeAni.cs 및 Assets/Game_Practice/MapDrop.cs 각 1개. 정확한 제외 경로는 VALIDATION.json에 있습니다.

`Assets/_ConeAni.cs`는 Animator 상태 제어, `Assets/Game_Practice/MapDrop.cs`는 낙하·반동 연출을 위한 보조 코드입니다. 사용자에게 외부 제공 코드가 없다는 확인을 받았고, 두 파일을 추가한 [3ca800ba54a0aa200dc4c35e2dec1b2c77c940fa](https://github.com/als79gur49/2025-2TeamProject/commit/3ca800ba54a0aa200dc4c35e2dec1b2c77c940fa)는 GitHub author 계정 als79gur49에 연결됩니다. 계정 연결만으로 저작권을 증명하지는 않지만, 출처 불명이나 권리 우려를 제외 사유로 삼지 않습니다. 승인된 핵심 소스 폴더 `Assets/Script/` 밖의 보조 코드라는 범위상 이유로 제외했고 파일을 추가하지 않았습니다.

외부 자산·폰트·이미지·오디오·모델·셰이더·씬·프리팹·애니메이션·ScriptableObject 실제 데이터·meta·DLL, 원본 .git, 개발도구 설정, 원본 작업문서를 제외했습니다. ScriptableObject를 정의하는 자체 C# 코드는 포함하되 직렬화된 실제 데이터는 제외했습니다. 자체 코드의 외부 API 참조는 유지했습니다.

[MANIFEST.csv](MANIFEST.csv)는 포함 소스의 원본 blob SHA-1, 크기, 로컬 SHA-256와 보조 파일 해시를 기록합니다. [VALIDATION.json](VALIDATION.json)은 실제 파일 집합, 원본 SHA/크기, 허용 목록, 금지 경로, 비밀 패턴 검사 결과를 기록합니다. 검사는 정의된 패턴의 탐지 결과이며 모든 형태의 비밀 부재를 보장하지 않습니다. 자기참조 해시 한계는 VALIDATION.json에 명시했습니다.

공개 사본 저장소: [als79gur49/2025-2TeamProject-code-portfolio](https://github.com/als79gur49/2025-2TeamProject-code-portfolio). 사용자가 승인한 418개 파일을 원본 이력 없이 새 저장소에 게시하는 범위입니다. 원본 저장소는 Private로 유지합니다.

정확한 경로별 허용 목록 .gitignore를 작성했습니다. 로컬 Git 초기화, 원본 저장소 수정·공개 설정 변경, 새 라이선스 추가를 하지 않았고, .gitattributes를 만들거나 인코딩·개행을 정규화하지 않았습니다. VALIDATION.json은 게시용 파일 집합의 사전 검증 기록입니다. 실제 게시 성공과 원격 전체 대조 결과는 사본 밖 FINAL-VERIFICATION.json에 기록해 검증 파일의 자기참조를 피합니다.

팀 담당과 Git 근거는 [CONTRIBUTIONS.md](CONTRIBUTIONS.md)를 참조하세요.

