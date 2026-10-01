# 기여와 근거

## 사용자 확인

사용자 프로젝트명은 Urban Tour입니다. 사용자 확인 담당은 김종우(기획), 권민혁(프로그래밍), 진현우(그래픽)입니다. 팀원의 코드·이름·프로젝트 설명을 포트폴리오로 공개하는 데 동의했다고 사용자에게 확인했습니다. 이는 사용자 진술이며 별도 동의서나 팀원 개별 확인을 Git으로 검증한 것은 아닙니다.

사용자는 수업·외부 예제·타인 제공 코드가 없다고 답했고, TeamProject Developer와 추가 Git 작성자 설정도 학교 컴퓨터에서 사용한 본인 설정이라고 확인했습니다. 원본에 외부 라이브러리/예제와 자산이 존재하는 사실과 구분하며 해당 외부 파일은 사본에서 제외했습니다.

질문에 제시된 철자는 `alsgur7949`, 사용자 답변의 철자는 `alsugr7949`입니다. 원본 Git의 실제 철자 `alsgur7949`를 유지합니다. 철자 차이로 새 인물을 만들거나 작성자 이름을 바꾸지 않았습니다.

## Git 검증

선택 커밋의 조상 이력 194개를 GitHub commits API 두 페이지로 조회했습니다. 아래 두 통계는 같은 이력을 서로 다른 필드로 집계한 것입니다.

| GitHub 연결 author 계정 | 커밋 수 |
| --- | ---: |
| als79gur49 | 184 |
| 연결 계정 없음 | 10 |
| 합계 | 194 |

계정 미연결 10개는 원시 Git author 이름이 TeamProject Developer인 9개와 alsgur7949인 1개입니다. 따라서 선행 검토의 “184 계정 + 9 TeamProject Developer + 1 alsgur7949”는 계정과 원시 작성자 이름을 함께 분류한 요약으로 해석됩니다. 이를 원시 Git 이름별 수라고 표현하지 않습니다.

| 원시 Git commit.author.name (원본 철자) | 커밋 수 | GitHub author 계정 연결 |
| --- | ---: | --- |
| als79gur49 | 176 | als79gur49 |
| alsgur7949 | 5 | 4개 als79gur49, 1개 미연결 |
| TeamProject Developer | 9 | 9개 미연결 |
| moonsoyi | 3 | 3개 als79gur49 |
| 권민혁 | 1 | 1개 als79gur49 |

`moonsoyi`는 Git에서 관찰된 이름 문자열이고 같은 GitHub 계정에 연결됩니다. 별도 팀원이나 새로운 사람이라고 추정하지 않았습니다. 계정 연결만으로 물리적 작업자를 증명할 수 없으며, 사용자에게 명시적으로 질문한 별칭의 본인 설정 확인과 구분합니다. 커밋 수로 인간 기여 비율이나 기획·그래픽 작업량을 산정하지 않습니다.

## 커밋과 파일에서 관찰되는 프로그래밍 작업

다음은 실제 커밋의 변경 파일 목록 및 고정 커밋의 소스를 함께 확인한 근거입니다. 담당자 역할은 위 사용자 확인에서 가져왔으며, 커밋 메시지에 있는 성능·완료·테스트 표현을 재검증된 결과로 옮기지 않습니다.

| 작업 | 실제 커밋과 변경 파일 근거 | 고정 사본에서 확인되는 구조 |
| --- | --- | --- |
| 마나 제한 카드 선택 | [122ac2c](https://github.com/als79gur49/2025-2TeamProject/commit/122ac2cb46c1f46681e4e4495fdc40300a80cba0): CardValueInfo.cs, EnemyAIController.cs, KnapsackCardSelector.cs 변경 | 휴리스틱 가치 평가 + 0/1 배낭 DP와 역추적 |
| 카드 평가·후보 위치 탐색 개선 | [9dc4b7f](https://github.com/als79gur49/2025-2TeamProject/commit/9dc4b7f6ffe48bd3c0d65b5373d550c30bb703a8): EnemyAIController.cs, GridController.cs, AreaShapeDefinition.cs 등 변경 | 필드 상태 평가와 카드 실행 메서드 분리, 팀별 위치 조회 |
| 유닛 판단·실행 분리 | [e3fb6c4](https://github.com/als79gur49/2025-2TeamProject/commit/e3fb6c48bc6f54d6fec4dbca406f78e9e1034f7f): IUnitAI.cs, BasicUnitAI.cs, Unit.cs, UnitService.cs 등 변경 | IUnitAI.DecideAction의 ActionDecision을 Unit 실행 흐름에서 사용 |
| 카드 서비스 수동 DI | [ecf7a3a](https://github.com/als79gur49/2025-2TeamProject/commit/ecf7a3ac0ee6a67c74dfee8805bf7a6cf08637df): CardServiceManager.cs, CardHandManager.cs, CardSpawnService.cs, SpawnValidator.cs 등 변경 | 서비스 초기화와 외부 주입; ServiceLocator도 함께 사용 |
| 카드팩 보상 이벤트·에디터 도구 | [8b1f532](https://github.com/als79gur49/2025-2TeamProject/commit/8b1f53250f18e622b71ca302cfda816433d14852): CardHandDebugWindow.cs 추가 | 이벤트 채널 정의 C#과 에디터 손패 조작 도구; 실제 채널 asset 제외 |

위 네 기능 커밋과 고정 커밋은 조회 결과 GitHub author 계정 als79gur49에 연결됩니다. 6단계 턴, 그리드 이동/전투, 다양한 카드효과, ServiceLocator와 수동 DI는 README의 파일 경로에서 직접 읽을 수 있습니다. 인간 기여를 파일 전체의 단독 작성이라고 단정하거나 AI 공동작성 메타데이터를 인간 기여 비율로 계산하지 않습니다. 일부 실제 커밋 메시지에는 Claude 공동작성 표기가 있으며 이는 도구 활용 흔적입니다.

## 기간과 제출 상태

사용자는 개발기간을 **2025년 9~12월**로 확인했습니다. Git author 날짜의 관찰 범위는 별도로 2025-09-06T04:25:25Z ~ 2025-12-12T17:46:12Z입니다. 실제 개발의 정확한 시작·종료일, 수업 제출일, 공식 최종 제출본은 확인하지 않았습니다. 사용자가 선택한 최신 기준은 feature/carddata-refactoring의 고정 커밋이며, main보다 158커밋 앞선 사실과 공식 제출본 여부는 별개입니다.

## 보조 코드 제외의 근거

`Assets/_ConeAni.cs`는 Animator 상태 제어, `Assets/Game_Practice/MapDrop.cs`는 낙하·반동 연출을 위한 보조 코드입니다. 사용자에게 외부 제공 코드가 없다는 확인을 받았고, 두 파일을 추가한 [3ca800ba54a0aa200dc4c35e2dec1b2c77c940fa](https://github.com/als79gur49/2025-2TeamProject/commit/3ca800ba54a0aa200dc4c35e2dec1b2c77c940fa)는 GitHub author 계정 als79gur49에 연결됩니다. 계정 연결만으로 저작권을 증명하지는 않지만, 출처 불명이나 권리 우려를 제외 사유로 삼지 않습니다. 승인된 핵심 소스 폴더 `Assets/Script/` 밖의 보조 코드라는 범위상 이유로 제외했고 파일을 추가하지 않았습니다.

루트 CardUIRefactored_Improved_Part1/2 및 backup_carddata의 코드는 별도 개선안·백업으로서 현행 구현 열람 범위에서 제외했습니다. 외부 제공 코드나 권리 문제가 확정된 파일이라고 분류한 것이 아닙니다. DOTween/Pro, Layer Lab 및 Unity TutorialInfo 코드는 외부 패키지·안내 샘플 소속으로 구분해 제외했습니다.

## 기록 범위

원본 작성자 철자와 코드·경로·바이트를 보존합니다. 이메일 주소 등 불필요한 Git 개인정보를 이 사본의 문서에 싣지 않습니다. 원본 Git 저장소나 원본 작업문서는 포함하지 않습니다. 새 라이선스나 재배포 허락을 이 문서로 추가하지 않았습니다.

