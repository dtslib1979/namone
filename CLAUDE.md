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