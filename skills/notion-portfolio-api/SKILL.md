---
name: notion-portfolio-api
description: "Notion 도구 사용법, DB 스키마 레퍼런스, 블록 구문 레퍼런스. 시스템 간 관계와 발행 흐름은 knowledge-ops 스킬을 참조. 트리거: notion_* 도구 사용 시, Notion DB 스키마/property/ID 확인 시, 블록 구문 확인 시."
---

# Notion Portfolio API — 도구 레퍼런스

## 역할

Notion 도구의 사용법, DB 구조, 블록 구문 레퍼런스를 다룬다.
Obsidian과의 관계, 발행 기준, 작성 루트는 **knowledge-ops 스킬**에 정의되어 있다.

---

## 인증

- 토큰 우선순위: NOTION_API_KEY (preferred) → NOTION_TOKEN
- 토큰 값 절대 출력 금지
- write 작업 전 반드시 `notion_validate_access` 실행
- 401 → NOTION_API_KEY 확인, gateway 재시작
- 403 → Notion UI에서 해당 페이지/DB를 integration에 공유

---

## Notion 페이지 구조

### Portfolio Home (문서 허브)
- ID: `YOUR_PORTFOLIO_HOME_PAGE_ID`
- 역할: 작성·관리 공간. 모든 하위 DB와 독립 페이지의 부모

### YOUR_NAME · Portfolio (메인 페이지 — 탐색 진입점)
- ID: `YOUR_PORTFOLIO_MAIN_PAGE_ID`
- **전체 교체 금지. block insert만 사용**

---

## DB 스키마

| DB | anchor page ID | DB ID |
|---|---|---|
| Projects | `YOUR_PROJECTS_SECTION_PAGE_ID` | `YOUR_PROJECTS_DB_ID` |
| Case Studies | `YOUR_CASE_STUDIES_SECTION_PAGE_ID` | `YOUR_CASE_STUDIES_DB_ID` |
| Research/Notes | `YOUR_RESEARCH_NOTES_SECTION_PAGE_ID` | `YOUR_RESEARCH_NOTES_DB_ID` |
| Domains | — | notion_search "Domains" filter_type=database 로 조회 |

### Relation Chain
```
Domain → Project (Hub) → Case Study (Narrative)
                       → Research / Notes (Reference)
```

### Domain Taxonomy (7개)
AI · Coding · Finance · Productivity · SNS Operations · Systems·Workflow · Soft Skills & Leadership

### Visibility 체계
Internal → Curated → Public → Featured

### Property 핵심
- **Projects**: Name, Summary, Status, Visibility, Domain(s), Tags, Start Date
- **Case Studies**: Name, Project [relation], Status, Visibility, Domain(s), Tags
- **Research/Notes**: Name, Summary, Domain(s), Related Project(s), Content Type, Status, Visibility, Tags

---

## 도구 사용 가이드

### Read (안전)
| 도구 | 용도 |
|------|------|
| notion_validate_access | write 세션 시작 시 |
| notion_search | 중복 확인, ID 조회 |
| notion_get_page_meta | 구조 확인 |
| notion_get_page_markdown | 내용 읽기 |
| notion_list_child_pages | 하위 목록 |
| notion_query_data_source | DB 쿼리 |
| notion_get_block_ids | 블록 ID 조회 (insert_after용) |

### Write (validated access 필요)
| 도구 | 용도 | 주의 |
|------|------|------|
| notion_create_page_markdown | 새 페이지 | 중복 확인 후 |
| notion_update_page_markdown | 전체 교체 | 텍스트만 있는 페이지에만 |
| notion_update_page_properties | 메타데이터만 | 내용 미변경 |
| notion_archive_page | Soft-delete | |
| notion_append_block_markdown | 끝에 추가 | 기존 블록 보존 |
| notion_insert_block_after | 특정 블록 뒤에 삽입 | get_block_ids 먼저 |

### 안전 규칙
1. validate before write
2. read before write
3. archive > delete
4. 중복 생성 금지 (search 먼저)
5. YOUR_NAME · Portfolio 메인 페이지 → **전체 교체 절대 금지**

---

## 쓰기 안전 규칙

- callout/toggle/page mention이 있는 기존 페이지 → `update_page_markdown` 금지
- 텍스트만 있는 단순 페이지 → `update_page_markdown` 사용 가능
- 기존 페이지에 추가 → `append_block_markdown`
- 위치 지정 삽입 → `insert_block_after` (get_block_ids로 ID 먼저 조회)

---

## 블록 구문 요약

Plugin v3 기준. **상세 구문 레퍼런스 → `references/block-syntax.md`**

### Standard Markdown → Notion
`#/##/###` heading · `- ` bullet · `1. ` numbered · `- [ ]` to_do · `> ` quote · `---` divider · `` ```lang ``` `` code · `![alt](url)` image · `$$expr$$` equation · `| | |` table

### Custom Syntax `[[ ]]` → Notion 전용 블록
- `[[ text ]]` callout (💡)
- `[[! text ]]` callout 경고 (⚠️, red)
- `[[> title ]]` toggle (빈)
- `[[> title ]]{` ... `}]` toggle + children
- `[[@ page_id | label ]]` page mention (인라인/블록 모두)
- `[[toc]]` table_of_contents
- `[[breadcrumb]]` breadcrumb
- `[[bookmark: url | caption]]` bookmark
- `[[columns]]` ... `[[column]]` ... `[[/columns]]` 다단 레이아웃
- `[[synced]]{...}]` synced_block 원본

### API 제약
- image/video/audio/file/pdf: external URL만 (Notion-hosted는 UI 전용)
- Max blocks per call: 100개
- Max nesting depth: 2단계

---

## 에러 대응

| 코드 | 원인 | 대응 |
|------|------|------|
| 401 | 토큰 무효 | NOTION_API_KEY 확인, gateway 재시작 |
| 403 | 권한 없음 | Notion UI → Share → integration 초대 |
| 404 | ID 오류/미공유 | ID 확인, 공유 상태 확인 |
| 429 | Rate limit | 대기 후 재시도, 루프 금지 |

---

## 작성 기준

- 밀도 우선: 최소 1줄 요약 + 본문 핵심 5~8문장
- Project: What / Status / Scope / Links / Why (허브, 상태 파악용)
- Case Study: Context / My Role / Key Decisions / Contributions / Learned / Next Step (서사)
- Project/Case Study: 1인칭 기본. Research/Notes: 중립 서술 허용.

## Notion API 2026-03-11 변경
- `archived` → `in_trash`로 대체
