---
name: knowledge-ops
description: >
  Obsidian + Notion 이중 운영 체계의 상위 규칙.
  Obsidian이 중심이고 Notion은 취사선택 발행 레이어.
  트리거: 콘텐츠 작성/정리/발행/업데이트 요청 시, Obsidian↔Notion 운영 판단이 필요할 때 이 스킬을 먼저 로드.
---

# Knowledge Ops — 이중 운영 체계

## 핵심 원칙

1. **Obsidian이 중심이다.** 모든 콘텐츠의 원본은 Obsidian에 존재한다.
2. **Notion은 발행 레이어다.** Obsidian의 콘텐츠 중 선별하여 Notion에 재구성한다.
3. **발행은 지시 시에만.** ReS가 Notion에 올리라고 할 때만 발행한다.
4. **재구성이지 복사가 아니다.** Notion에 올릴 때 Obsidian 원문을 그대로 옮기지 않는다. Notion의 구조와 목적에 맞게 재구성한다. Obsidian보다 더 길어질 수도 있다.

---

## 시스템 역할 정의

### Obsidian (중심) — ~/vaults/YOUR_OBSIDIAN_VAULT

나의 모든 콘텐츠의 원본. PARA 구조.

- **Projects/** — 마감 또는 산출물이 있는 활성 작업. 진행 중인 프로젝트, 달성할 목표가 있는 것
- **Areas/** — 종료 없이 지속되는 관심 영역. AI, Coding, Finance, Productivity, 건강, 일상 기록 등
- **Resources/** — 재사용 가능한 참고 자료. 프레임워크, 템플릿, 도구 노트, 외부 자료 정리
- **Archive/** — 비활성/완료된 것. 더 이상 발전시키지 않지만 보존할 가치가 있는 것
- **_Atlas/** — 내비게이션 허브. Home.md = 메인 진입점
- **_System/** — 운영 문서, 거버넌스, 로그
- **_Assets/** — 첨부 파일
- **_Trash/** — 소프트 삭제

### Notion (발행 레이어)

Obsidian에서 취사선택한 콘텐츠를 재구성하여 발행하는 곳.

- **Portfolio Home** (ID: YOUR_PORTFOLIO_HOME_PAGE_ID)
  문서 허브. 메인 페이지 노출 전 작성·관리하는 공간. 모든 하위 DB와 독립 페이지의 부모.
  - Domains DB — 7개 지식 영역 분류 (taxonomy)
  - Projects DB — 이니셔티브 허브. 개요·상태·마일스톤 중심
  - Case Studies DB — 서사·의사결정·회고 중심. Project에 링크
  - Research / Notes DB — 학습 로그, 리서치, 아이디어

- **YOUR_NAME · Portfolio** (ID: YOUR_PORTFOLIO_HOME_PAGE_ID)
  탐색 진입점. Portfolio Home의 콘텐츠를 쉽게 찾기 위한 곳.

### Archive 차이

- **Obsidian**: 완료된 프로젝트는 Archive/ 폴더로 이동. PARA 체계의 일부.
- **Notion**: 완료 프로젝트도 DB 안에 유지하고 Status로 구분. `notion_archive_page`는 soft-delete(trash)용.
- "archive 해줘" 요청 시 → 문맥으로 구분.

### Areas vs Domains 비대칭

Obsidian Areas와 Notion Domains는 1:1 대응이 아니다.
Obsidian은 개인 운영 중심이라 더 넓고 생활 밀착적일 수 있고 (Lifestyle, Daily Notes 등),
Notion은 포트폴리오/탐색 중심이라 압축된 taxonomy를 사용한다 (7개 Domains).
Obsidian의 모든 Area가 Notion Domain에 대응하지 않으며, 그래야 할 이유도 없다.

---

## 작업 흐름: 의사결정 트리

### 새 콘텐츠 작성 요청

```
요청이 들어왔다
├── 이 콘텐츠는 무엇인가?
│   ├── 개인 메모, 강의 노트, 일상 기록, 투자 분석, 학습 노트
│   │   → Obsidian에만 작성. 끝.
│   │
│   └── 그 외 (프로젝트, 기획, 설계, 분석, 회고 등)
│       → Obsidian에 먼저 작성
│       → 작성 완료 후 "Notion에도 올릴까요?" 물어보기
│       → ReS가 YES → Notion에 재구성하여 발행
│       → ReS가 NO → Obsidian에만 유지
```

### 기존 콘텐츠 업데이트 요청

```
업데이트 대상이 어디에 있는가?
├── Obsidian에만 있음
│   → Obsidian 업데이트. 끝.
│
├── Notion에만 있음 (역사적 이유로 Obsidian에 원본 없음)
│   → Obsidian에 원본 먼저 생성 or 확인
│   → 그 다음 Notion 업데이트
│
└── 양쪽 다 있음
    → Obsidian 원본 먼저 확인/업데이트
    → 그 다음 Notion 반영 (the user 지시 시)
```

### Notion 발행 흐름

```
ReS가 "Notion에 올려줘" 지시
│
├── 1. Obsidian 원본 확인 (최신 상태인지)
├── 2. Notion에 이미 존재하는지 확인 (notion_search)
│   ├── 존재 → 기존 페이지 업데이트
│   └── 미존재 → Portfolio Home 아래 해당 DB에 새 페이지 생성
├── 3. Notion에 맞게 재구성하여 작성
├── 4. DB property 설정 (Domain, Status, Visibility 등)
└── 5. YOUR_NAME · Portfolio 메인 페이지에 노출 (block insert)
```

---

## Notion 발행 기준

### Notion에 가야 하는 콘텐츠
- 포트폴리오에 포함할 프로젝트, 케이스 스터디
- 외부 공유가 필요한 정리된 문서
- 구조화된 DB relation이 필요한 항목
- ReS가 "올려줘"라고 지시한 것

### Obsidian에만 있으면 되는 콘텐츠
- 개인 메모, 일상 기록
- 강의 노트, 학습 노트
- 투자 분석, 기업 리서치
- 회의록, raw 자료
- 아직 정리되지 않은 초안/fragment

### 판단이 애매할 때
- ReS에게 물어본다: "Notion에도 올릴까요?"

---

## Notion 도구 제약

Notion 블록 생성 능력의 상세는 notion-portfolio-api 스킬을 참조.
plugin v3 기준 대부분의 블록 타입을 네이티브 지원한다.
column_list/column, synced_block, breadcrumb 포함.

### Notion API 2026-03-11 주요 변경
- `archived` 필드 → `in_trash`로 대체
- 아카이브 요청: `{ in_trash: true }`

---

## 쓰기 안전 규칙

- callout/toggle/page mention이 있는 기존 페이지 → `update_page_markdown` 전체 교체 금지
- 텍스트만 있는 단순 페이지 → `update_page_markdown` 사용 가능
- YOUR_NAME · Portfolio 메인 페이지 → 전체 교체 절대 금지. `append_block_markdown` 사용 (위치는 UI에서 조정)
- 새 페이지 → `create_page_markdown` 자유 사용
- 기존 페이지에 추가 → `append_block_markdown` (끝에 추가). Notion API는 블록 위치 지정 삽입 미지원 — 위치 조정은 UI에서 드래그
- validate before write / read before write / archive > delete

---

## 서술 원칙

### 1인칭 기본 (포트폴리오 / 프로젝트 / 경험 / 케이스 스터디)
- "나는 이 프로젝트를 리딩했다" (O)
- "ReS는 이 프로젝트를 리딩했다" (X)
- 내 역할, 내 기여, 내 의사결정으로 서술

### 중립 서술 허용 (개념 / 리서치 / 레퍼런스 / 거버넌스 / 강의 요약)
- 1인칭을 강제하지 않음
- 내용의 성격에 맞게 중립 서술 가능
- 예: "PARA 체계는 ~로 구성된다" (O), "Transformer는 ~를 기반으로 한다" (O)

---

## 하위 스킬 참조 규칙

이 스킬(knowledge-ops)을 로드한 상태에서:

- **Obsidian 내부 작업** (폴더 배치, 프론트매터, 노트 타입 판단)
  → `skills/obsidian-governance/SKILL.md` 참조
- **Notion 내부 작업** (DB 스키마, property 설정, ID 레퍼런스, 블록 구문)
  → `skills/notion-portfolio-api/SKILL.md` 참조
- 참조가 필요하면 해당 스킬 파일을 그때 읽는다

---

## YOUR_NAME · Portfolio 메인 페이지 운영

- ID: YOUR_PORTFOLIO_HOME_PAGE_ID
- 역할: 탐색 진입점
- **전체 교체 금지**

### 새 항목 노출 절차
1. Portfolio Home 아래 DB에 페이지 생성
2. the user 확인
3. `notion_get_block_ids`로 메인 페이지 블록 조회
4. `notion_append_block_markdown`으로 끝에 추가 후 Notion UI에서 원하는 위치로 드래그
5. 토글은 내용이 채워진 상태로 삽입
