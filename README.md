# Decision Case Pooling

AI와 함께 개발하며 내린 결정을 근거와 함께 축적하는 한국어 Agent Skill입니다.

하나의 결정은 YAML 메타데이터와 Markdown 본문을 갖는 하나의 파일이 됩니다. 후보를 모으고 보완한 뒤, 케이스 스터디와 포트폴리오의 재료로 사용할 수 있습니다.

## 설치

Codex의 스킬 설치 도구에 다음과 같이 요청하세요.

```text
$skill-installer https://github.com/yhoiy/decision-case-pooling 저장소 루트의 스킬을 설치해줘.
```

또는 Skills CLI로 설치할 수 있습니다.

```sh
npx skills add yhoiy/decision-case-pooling --skill decision-case-pooling
```

## 사용

개발 대화가 있는 작업에서 실행하세요.

```text
$decision-case-pooling 이번 작업에서 의사결정 사례 후보를 뽑아줘.
```

```text
$decision-case-pooling 이번 작업의 의사결정을 case-pool/에 저장해줘.
```

```text
$decision-case-pooling 기존 케이스에 방금 실행한 테스트 결과를 보완해줘.
```

접근 가능한 대화와 지정된 코드·검증 기록만 사용합니다. 과거의 모든 대화를 자동 수집하거나 백그라운드에서 실행하지 않습니다. 별도 MCP 서버나 Notion 연결은 필요하지 않습니다.

## 출력

```text
case-pool/
├── index.md
└── 2026-10-05-short-topic.md
```

YAML에는 `schema_version`, `id`, `title`, `project`, `work_date`, `recorded_at`, `updated_at`, `status`, `familiarity`, `tags`를 기록합니다. 날짜는 인용한 YYYY-MM-DD 문자열, 미확인 프로젝트·작업일은 null로 표현합니다. ID는 UUID v4이며 제목이나 파일명 변경 후에도 유지합니다.

- 상태: `candidate`, `needs-context`, `confirmed`, `written`
- 코드베이스·스택 익숙함: 각각 `unfamiliar`, `familiar`, `unknown`
- `written`은 글 정리 완료이며 공개 여부와 무관합니다.

본문은 상황 → 판단 계기 → 선택과 이유 → AI와 사용자의 역할 → 검증과 결과 → 회고 순서로 구성하고, 근거와 보완 질문을 덧붙입니다. 상세 포맷은 [템플릿](references/case-template.md)을 참고하세요.

## 기록 원칙

- 관찰 사실, 사용자가 설명한 이유, AI의 추정을 구분합니다.
- 검토하지 않은 대안이나 측정하지 않은 성과를 만들어 넣지 않습니다.
- 실패뿐 아니라 근거를 갖고 AI 제안을 채택한 사례도 기록합니다.
- 사용자 검토와 공개는 별개입니다. 저장 요청은 커밋·업로드 요청이 아닙니다.
- 이 공개 저장소는 스킬을 배포합니다. 실제 작업 기록은 사용자가 지정한 작업 공간에 저장합니다.

## 구성

- [SKILL.md](SKILL.md): 후보 선정·작성·저장 지침
- [references/case-template.md](references/case-template.md): 케이스 포맷
- [agents/openai.yaml](agents/openai.yaml): Codex 표시 정보

첫 배포 버전은 v0.1.0입니다. 형식과 설치 경로를 검증한 초기 버전이며, 사례 추출 품질은 실제 작업에 적용하며 개선합니다.
