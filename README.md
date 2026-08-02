English | [한국어](#first-principles-한국어)

# first-principles

A skill for structured first-principles thinking, built on the [Agent Skills](https://claude.ai/code) format (`SKILL.md` + frontmatter) shared by Claude Code, Codex CLI, Cursor, Gemini CLI, and other compatible coding agents. Instead of reasoning by analogy or convention, it decomposes a problem into irreducible ground truths and reasons back upward from there.

## Installation

Clone the repo, then copy it into whichever agent's skills directory you use:

```bash
git clone https://github.com/LisanalGaib7/first-principles.git
```

| Agent | Skills directory |
|---|---|
| Claude Code | `~/.claude/skills/` |
| Codex CLI | `~/.codex/skills/` |
| Cursor / others | check that agent's docs for its skills path |

```bash
cp -r first-principles ~/.claude/skills/first-principles   # Claude Code
cp -r first-principles ~/.codex/skills/first-principles    # Codex CLI
```

**Structure**

```
first-principles/
├── SKILL.md                    # skill definition (frontmatter + methodology)
├── examples/
│   └── architecture-review.md  # worked example: microservices decision
└── references/
    ├── elon-musk-examples.md   # SpaceX / Tesla case studies
    └── software-examples.md    # software engineering case studies
```

**How it triggers**

The `description` field in `SKILL.md`'s frontmatter is matched against how you phrase a request. It fires on prompts like "analyze from first principles", "question this design", "is there a better solution" — and, since this fork adds bilingual support, on Korean equivalents like "1원칙으로 분석", "가정을 의심".

**The 5-phase process**

1. **Problem Essence** — strip away implementation details to state the real problem and success criteria
2. **Challenge Assumptions** — list every assumption (technical / business / resource / historical) and test whether it's a real constraint or just convention
3. **Ground Truths** — isolate the facts that cannot be decomposed further (physics, business invariants, user needs)
4. **Reason Upward** — build the minimal solution that satisfies the ground truths, adding complexity only when it earns its place
5. **Validate** — trace every design decision back to a ground truth; find the weak links

**Output format**

Every analysis follows a fixed template: Problem Essence → Assumptions Challenged (table) → Ground Truths → Reasoning Chain → Conclusion.

**Worked example**

> Prompt: *"Diesel supply is tight right now — where should we source diesel from?"*

```markdown
## First Principles Analysis: Diesel Sourcing Under Tight Refining Supply

### 1. Problem Essence
**Core problem:** Secure diesel volume reliably, at a defensible total cost (price + logistics + risk)
**Success criteria:** No supply interruption at the required time and volume — not simply "lowest price"

### 2. Assumptions Challenged
| Assumption | Challenge | Evidence / How to Verify | Verdict |
|---|---|---|---|
| "Buy from regions with the most refining capacity" | Do those regions actually let the volume leave, or keep it for themselves first? | Structural capacity loss raises the odds producer nations prioritize domestic supply and restrict exports during a shortage | Modify |
| "Time the spot market for a good deal" | Can we wait for a dip and buy cheap? | 3-2-1 crack spread at an all-time high (~$64.58/bbl, July 2026); refining margins near $70/bbl | Discard |
| "Buy directly from refiners" | Do refiners have spare capacity to sell us more? | Refiners running at 92–95% utilization — no slack to allocate | Modify |
| "Local sourcing is always better" | Does proximity outweigh availability risk? | Refining capacity and inventory data point to a structural, not temporary, shortage — continuity risk dominates logistics savings | Keep |

### 3. Ground Truths
- Global refining capacity has structurally shrunk (permanent closures + war damage cut ~4.5M bbl/day, -5.4%, in Q2 2026)
- Refiners are near max utilization — no slack to absorb new demand
- US diesel inventories are near 5-year lows

### 4. Reasoning Chain
Structural capacity loss + record-low inventory + record-high margins → no source is "cheap" right now → the optimization target shifts from price to *certainty of supply* → lock in volume via contracts, diversify across sources

### 5. Conclusion
**Recommended approach:** Shift from spot buying to mid/long-term offtake agreements; select sourcing regions by export-restriction risk, not raw refining capacity; diversify across multiple suppliers
**Key insight:** "Where can we buy it cheap?" is the wrong question during a structural shortage — the right question is "where can we lock in volume?"
**Trade-offs acknowledged:** Long-term contracts may look expensive if margins later fall; diversification adds coordination overhead
```

## Credits

`first-principles` is adapted from [awesome-skills/first-principles-skill](https://github.com/awesome-skills/first-principles-skill) (MIT License), with bilingual (English/Korean) trigger phrases and output templates added, plus an Evidence/How-to-Verify column on the assumptions table so a Keep/Discard/Modify verdict requires an actual observation rather than a guess.

## License

MIT — see [LICENSE](LICENSE).

---

# first-principles (한국어)

구조화된 1원칙(First Principles) 사고 스킬. Claude Code, Codex CLI, Cursor, Gemini CLI 등 여러 코딩 에이전트가 공유하는 [Agent Skills](https://claude.ai/code) 포맷(`SKILL.md` + frontmatter) 위에 만들어져 특정 도구에 종속되지 않습니다. 유추나 관행에 기대는 대신, 문제를 더 쪼갤 수 없는 근본 사실까지 분해한 뒤 거기서부터 다시 추론해 올라갑니다.

## 설치

레포를 clone한 뒤, 쓰는 에이전트의 스킬 디렉터리에 복사하면 됩니다.

```bash
git clone https://github.com/LisanalGaib7/first-principles.git
```

| 에이전트 | 스킬 디렉터리 |
|---|---|
| Claude Code | `~/.claude/skills/` |
| Codex CLI | `~/.codex/skills/` |
| Cursor 등 | 해당 도구 문서에서 스킬 경로 확인 |

```bash
cp -r first-principles ~/.claude/skills/first-principles   # Claude Code
cp -r first-principles ~/.codex/skills/first-principles    # Codex CLI
```

**구조**

```
first-principles/
├── SKILL.md                    # 스킬 정의 (frontmatter + 방법론)
├── examples/
│   └── architecture-review.md  # 완성 예시: 마이크로서비스 도입 여부 분석
└── references/
    ├── elon-musk-examples.md   # 스페이스X, 테슬라 사례
    └── software-examples.md    # 소프트웨어 엔지니어링 적용 사례
```

**트리거 방식**

`SKILL.md` frontmatter의 `description` 필드가 요청 문구와 매칭되어 자동 실행됩니다. "analyze from first principles", "question this design", "is there a better solution" 같은 영어 문구뿐 아니라, 이 포크에서 추가한 "1원칙으로 분석", "가정을 의심" 같은 한국어 문구로도 트리거됩니다.

**5단계 프로세스**

1. **문제의 본질** — 구현 디테일을 걷어내고 진짜 문제와 성공 기준을 정의
2. **가정 도전** — 기술/비즈니스/리소스/역사적 가정을 전부 나열하고, 진짜 제약인지 그냥 관행인지 검증
3. **근본 사실** — 더 쪼갤 수 없는 사실(물리 법칙, 비즈니스 불변식, 유저 니즈)만 남김
4. **상향 추론** — 근본 사실을 만족하는 최소 해법을 만들고, 정당화될 때만 복잡도를 추가
5. **검증** — 모든 설계 결정이 근본 사실까지 역추적되는지 확인하고 약한 고리를 찾음

**출력 포맷**

모든 분석은 고정된 템플릿을 따릅니다: 문제의 본질 → 도전한 가정(표) → 근본 사실 → 추론 사슬 → 결론.

**실제 적용 예시**

> 질문: *"정유 공급이 타이트한 지금, 디젤을 어디서 소싱하는 게 좋을까?"*

```markdown
## 1원칙 분석: 정유 공급 타이트 국면에서의 디젤 소싱 전략

### 1. 문제의 본질
**핵심 문제:** 안정적인 물량과 합리적인 총비용(가격+물류+리스크)으로 디젤을 확보하는 것
**성공 기준:** 공급 중단 없이 필요 시점에 필요 물량을 받는 것 (단순히 "싸게 사는 것"이 아님)

### 2. 도전한 가정
| 가정 | 왜 의심하는가 | 근거/확인방법 | 판정 |
|------|--------------|--------------|------|
| "정제능력 큰 지역에서 사면 된다" | 그 지역이 실제로 물량을 내보낼까, 자국 우선으로 묶어둘까? | 정제능력이 구조적으로 축소된 상황에서는 생산국이 자국 공급을 우선해 수출을 제한할 가능성이 커짐 | 수정 |
| "현물시장에서 타이밍 봐서 유리하게 살 수 있다" | 눌렸다가 쌀 때 살 수 있나? | 2026년 7월 기준 3-2-1 크랙스프레드 사상 최고치(~$64.58/bbl), 마진 ~$70/bbl | 폐기 |
| "정유사에서 직접 사는 게 최선이다" | 정유사에 우리에게 더 팔 여유 물량이 있나? | 가동률 92~95% — 배분할 여유 캐파 없음 | 수정 |
| "가까운 곳에서 사는 게 무조건 유리하다" | 근접성이 조달 리스크보다 중요한가? | 정제능력·재고 데이터가 일시적이 아니라 구조적 부족을 가리킴 — 물류비 절감보다 공급 연속성 리스크가 더 큰 변수 | 유지 |

### 3. 근본 사실
- 전 세계 정제능력이 구조적으로 축소 중 (영구 폐쇄 + 전쟁 피해로 2026년 2분기 일산 450만 배럴, -5.4% 감소)
- 정유사 가동률이 92~95%로 이미 상한 근접 → 여유 물량 없음
- 미국 디젤 재고가 5년래 최저치

### 4. 추론 사슬
구조적 캐파 축소 + 재고 최저 + 마진 사상최고 → 지금 "싸게" 구할 소스는 없음 → 최적화 목표가 가격에서 확보 가능성으로 전환 → 계약으로 물량을 먼저 잠그고 소스를 다변화

### 5. 결론
**권고안:** 현물 구매 대신 중장기 오프테이크 계약으로 물량 우선 확보, 소싱 지역은 정제능력이 아니라 수출규제 리스크로 재선정, 복수 소스 다변화
**핵심 통찰:** "어디서 싸게 살까"는 구조적 공급 부족기엔 성립하지 않는 질문. "어디서 물량을 잠글 수 있나"가 맞는 질문
**감수하는 트레이드오프:** 장기계약은 이후 마진 하락 시 비싸 보일 수 있음, 다변화는 관리 복잡도를 늘림
```

## 출처

`first-principles`는 [awesome-skills/first-principles-skill](https://github.com/awesome-skills/first-principles-skill)(MIT License)을 기반으로, 영어/한국어 이중언어 트리거 문구와 출력 템플릿을 추가한 버전입니다. 여기에 가정 표에 "근거/확인방법" 열을 더해, 판정(유지/폐기/수정)을 내리려면 추측이 아니라 실제로 관측한 근거가 있어야 하도록 만들었습니다.

## 라이선스

MIT — [LICENSE](LICENSE) 참고.
