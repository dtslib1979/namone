# JUSTINO 에이전트 프로토콜 v1.0

> Shopping Mall Branch — 쇼핑몰 프랜차이즈 브랜치
> 전환: namone (부동산 길드장) → justino (쇼핑몰) / 2026-03-07
> namone 길드장 역할 → namoneygoal로 흡수 완료

---

## 헌법 제1조: 레포지토리는 소설이다

> **모든 레포지토리는 한 권의 소설책이다.**
> **커밋이 문장이고, 브랜치가 챕터이고, git log --reverse가 줄거리다.**

- 삽질, 실패, 방향 전환 전부 남긴다. squash로 뭉개지 않는다.
- 기능 구현 과정 = 플롯 (문제→시도→실패→전환→해결)
- 레포 서사 → 블로그/웹툰/방송 콘텐츠로 파생 (액자 구성)

---

## 헌법 제2조: 매트릭스 아키텍처

> **모든 레포지토리는 공장이다.**
> **가로축은 재무 원장(ERP)이고, 세로축은 제조 공정(FAB)이다.**

### 4대 원칙

1. **삭제는 없다, 반대 분개만 있다** — `git revert`로 정정. `reset --hard` 금지.
2. **증빙 없는 거래는 없다** — 커밋 메시지에 이유와 맥락.
3. **BOM 확인 후 착공한다** — 의존성/에셋 명세 먼저, 공정 순서 명시 후 실행.
4. **재공품을 방치하지 않는다** — WIP 브랜치와 큐는 정기적으로 소화한다.

---

## 1. Branch Identity

| 항목 | 값 |
|------|-----|
| **ID** | justino |
| **역할** | 쇼핑몰 프랜차이즈 브랜치 |
| **본사** | dtslib1979/dtslib-branch |
| **보일러플레이트** | gohsy-fashion (4채널 루프백) |
| **상태** | active |
| **이력** | namone → justino (2026-03-07) |

---

## 2. 커머스 구조

```
보일러플레이트: gohsy-fashion
├── 상품 등록 → PRODUCT_CARD.json
├── 에셋 생성 → parksy-image / parksy-audio
├── 채널 배포 → 온라인 스토어 / YouTube / 쇼룸
└── 분석 → 다음 상품 기획
```

---

## 3. HQ 연동

| 항목 | 값 |
|------|-----|
| **본사 레포** | dtslib1979/dtslib-branch |
| **브랜치 ID** | justino |
| **상태** | active |
| **공개** | public |
| **레지스트리** | `hq/registry/branches.json` |

---

## 4. 전환 기록

```
namone (부동산 길드장)
  │
  ├── 길드장 역할 → namoneygoal로 흡수 (2026-03-07)
  │   namoneygoal = 길드장 + 길드 운영 겸임
  │
  └── namone 레포 → justino로 리네임 + 쇼핑몰 전환
      justino = 쇼핑몰 프랜차이즈 브랜치
```

---

## 5. 커밋 컨벤션

```
feat: 새 기능/상품 추가
fix: 버그 수정
docs: 문서 업데이트
content: 콘텐츠 추가/수정
commerce: 커머스 관련 작업
```

---

*Version: 1.0*
*Last Updated: 2026-03-07*
*Affiliation: DTSLIB HQ (Shopping Mall Branch)*
