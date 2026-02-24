# NAMONE 에이전트 프로토콜 v1.0

---

## 헌법 제1조: 레포지토리는 소설이다

> **모든 레포지토리는 한 권의 소설책이다.**
> **커밋이 문장이고, 브랜치가 챕터이고, git log --reverse가 줄거리다.**

- 삽질, 실패, 방향 전환 전부 남긴다. squash로 뭉개지 않는다.
- 기능 구현 과정 = 플롯 (문제→시도→실패→전환→해결)
- 레포 서사 → 블로그/웹툰/방송 콘텐츠로 파생 (액자 구성)

### 서사 추출 명령

```bash
narrative-extract.py --repo .                    # 이 레포 줄거리
narrative-extract.py --repo . --format synopsis  # 시놉시스
narrative-extract.py --repo . --format blog      # 블로그 원고
narrative-extract.py --repo . --climax           # 전환점만
narrative-extract.py --all ~                     # 28개 레포 연작 인덱스
```

### 서사 분류

| 커밋 유형 | 서사 | 의미 |
|-----------|------|------|
| `feat:` / 기능 추가 | 시도 | 주인공이 무언가를 만든다 |
| `fix:` / 버그 수정 | 삽질 | 예상대로 안 됐다 |
| `migration` / 전환 | 전환 | 버리고 다른 길을 간다 |
| `rewrite` / v2 | 각성 | 처음부터 제대로 다시 한다 |
| `refactor:` | 성장 | 같은 일을 더 잘하게 됐다 |
| `docs:` | 정리 | 지나온 길을 돌아본다 |

---

## ⚙️ 헌법 제2조: 매트릭스 아키텍처

> **모든 레포지토리는 공장이다.**
> **가로축은 재무 원장(ERP)이고, 세로축은 제조 공정(FAB)이다.**

### 가로축: 재무 원장 (ERP 로직)

커밋은 전표다. 한번 기표하면 수정이 아니라 반대 분개로 정정한다.

| 회계 개념 | Git 대응 | 예시 |
|-----------|----------|------|
| 전표 (Journal Entry) | 커밋 | `feat: 새 기능 구현` |
| 원장 (General Ledger) | `git log --reverse` | 레포 전체 거래 이력 |
| 계정과목 (Account) | 디렉토리 | `tools/`, `scripts/`, `assets/` |
| 회계 인터페이스 | 크로스레포 동기화 | 명시적 스크립트/매니페스트 |
| 감사 추적 (Audit Trail) | Co-Authored-By | AI/Human 협업 기록 |

**원칙:**
1. **삭제는 없다, 반대 분개만 있다** — `git revert`로 정정. `reset --hard` 금지.
2. **모든 거래에 증빙이 있다** — 커밋 메시지에 이유와 맥락 기록.
3. **레포 간 전이는 인터페이스다** — 크로스레포 데이터 이동은 명시적 스크립트/매니페스트로.

### 세로축: 제조 공정 (FAB 로직)

레포는 반도체 팹이다. 원자재(아이디어)가 들어와서 완제품(콘텐츠)이 나간다.

| 제조 개념 | 레포 대응 | 예시 |
|-----------|----------|------|
| BOM (자재 명세) | 의존성 + 에셋 목록 | `pubspec.yaml`, `package.json`, `assets/` |
| 라우팅 (공정 순서) | 파이프라인 스크립트 | 빌드→테스트→배포 순차 실행 |
| WIP (재공품) | 브랜치 + Queue | `claude/*` 브랜치, `_queue/` |
| 수율 (Yield) | 빌드 성공률 | CI 통과율, 테스트 커버리지 |
| MES (제조실행) | 자동화 스크립트 | 동기화, 추출, 배포 도구 |
| 검수 (QC) | 테스트 + 리뷰 | `tests/`, 체크리스트 |

**원칙:**
4. **BOM 없이 착공하지 않는다** — 의존성과 에셋을 먼저 명세한다.
5. **공정에는 순서가 있다** — 파이프라인 스크립트에 단계를 명시한다.
6. **재공품을 방치하지 않는다** — WIP 브랜치와 큐는 정기적으로 소화한다.

### 교차점: JSON 매니페스트

가로축과 세로축이 만나는 곳에 JSON이 있다. 매니페스트는 공정 기록이자 거래 증빙이다.

```
app-meta.json      = 제품 사양서
state.json         = 공정 현황판
*.youtube.json     = 출하 전표
*-SOURCES.md       = 원자재 입고 대장
```

### Claude 지침

> **개발/업데이트 작업 시작 시, 해당 작업이 매트릭스의 어느 축에 해당하는지 식별하라.**
> BOM 미확인 착공, 증빙 없는 커밋, WIP 방치를 감지하면 경고하라.
> 새 파일/도구 추가 시 해당 매니페스트(JSON/MD) 업데이트를 확인하라.

> **코드를 짜는 게 아니라 공장을 돌리고 있다.**
> **다만 그 공장의 원장이 git이고, 라인이 파이프라인일 뿐이다.**

---


> 이 문서는 Claude Code가 namone 레포지토리에서 작업할 때 따라야 하는 가이드입니다.

---

## 1. Branch Identity (2-Axis System)

| 축 | 값 | 설명 |
|----|-----|------|
| **Governance** | `collaborator` | HQ와 강하게 연동. 구조/룰/업데이트 HQ 주도 |
| **Cognitive** | `creator` | 콘텐츠 생산 중심, 부동산 전문 지식 |

### HQ Access 권한
```
✅ templates    - 페이지/컴포넌트 템플릿
✅ sync         - HQ 동기화 시스템
✅ claude-code  - Claude Code 에이전트 접근
✅ broadcast    - 방송/강의 시스템
```

### 캐릭터 프로필
- **정체성**: 시흥 남원골 부동산 전문 중개인
- **역할**: 부동산 길드(namoneygoal) 길드장
- **전략**: AI 워키토키 활용, 설명 자산화

---

## 2. 프로젝트 개요

### 목적
김남원 공인중개사 - 부동산 길드 길드장 브랜치

### Focus 영역
- 시흥 지역 부동산
- AI 활용 매물 분석
- 부동산 길드 운영

### 기술 스택
- 순수 정적 사이트 (HTML/CSS/JS)
- GitHub Pages 호스팅

---

## 3. HQ 연동

이 프로젝트는 **DTSLIB HQ**에서 관리됩니다.

| 항목 | 값 |
|------|-----|
| **본사 레포** | dtslib1979/dtslib-branch |
| **브랜치 ID** | namone |
| **상태** | active |
| **공개** | public |
| **길드** | namoneygoal (길드장) |
| **레지스트리** | `hq/registry/branches.json` |

---

## 4. 길드장 역할

### namoneygoal 길드와의 관계
- **역할**: 부동산 길드 길드장
- **권한**: 멤버 관리, 콘텐츠 방향 설정
- **책임**: 길드 운영, 업계 네트워크

### 길드장으로서의 의무
1. 길드 멤버 모집 (12슬롯)
2. 업계 관찰 및 기록
3. AI 워키토키 활용 시범

---

## 5. 폴더 구조

```
namone/
├── index.html              # 메인 페이지
├── config.json             # 설정 파일
├── branch.json             # 브랜치 설정
├── CLAUDE.md               # 이 문서
│
├── assets/
│   ├── manifest.json       # PWA 설정
│   └── icons/
│
├── articles/               # 부동산 아티클
├── card/                   # 명함 페이지
├── staff/                  # 스태프 모드
└── studio/                 # 스튜디오
```

---

## 6. 커밋 컨벤션

```
feat: 새 기능 추가
fix: 버그 수정
docs: 문서 업데이트
style: 디자인 변경
content: 콘텐츠 추가/수정
guild: 길드 관련 작업
```

커밋 메시지 끝:
```
Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
```

---

## 7. 작업 시 주의사항

1. 수정 전 반드시 `git pull` 실행
2. 부동산 관련 법적 정보 주의
3. 개인정보 노출 주의
4. namoneygoal 길드와 일관성 유지

---

*Version: 1.0*
*Last Updated: 2026-02-06*
*Affiliation: DTSLIB HQ (Collaborator) / namoneygoal Guild Master*