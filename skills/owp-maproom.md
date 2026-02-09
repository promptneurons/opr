# OWP Map Room Skill

Organizational Weather Prediction (OWP) dashboard skill. Maps NWP forecasting patterns to organizational intelligence.

## Source Reference

Adapted from Haby's Weather Map Room: https://www.theweatherprediction.com/maproom/

Note: whigdev.com forum (WX Map Room thread) is down - same host as Sand Dollar.

## Organizational Map Room

### Synoptic Analysis (Current State)

| NWP Layer | Org Equivalent | Data Source | Script |
|-----------|----------------|-------------|--------|
| Surface | Gate Status | quality-gate.sh | `./scripts/quality-gate.sh` |
| 850 mb | Sprint Context | .beads/open.yaml | `cat .beads/open.yaml` |
| 700 mb | Resources | markov-blanket.sh | `./scripts/markov-blanket.sh` |
| 500 mb | Decisions | decision-queue.md | `cat projects/decision-queue.md` |
| 300 mb | Strategic | MEMORY.md | `cat MEMORY.md` |

### Radar/Satellite (Real-Time Monitoring)

| NWP | Org Equivalent | Data Source |
|-----|----------------|-------------|
| Radar | Audit Log | data/audit-log.jsonl |
| IR Satellite | Session History | memory/*.md |
| Visible | Active Conversations | Current session |
| Water Vapor | Token/Cost Flow | API usage stats |

### Severe Weather Indicators

Map to organizational risk indicators:

#### Moisture → Resources
- Surface Dewpoint → Available budget
- Column RH → Team capacity
- Precipitable Water → Pipeline depth

#### Instability → Urgency
- CAPE → Backlog pressure
- Lifted Index → Blocker severity
- Surface Temp → Activity level

#### Wind Shear → Conflict/Change
- 850 mb wind → Team velocity
- Jet Stream → Strategic shifts
- EHI → Change risk index

#### Lift → Momentum
- 700 mb UVV → Sprint velocity
- Vorticity → Decision throughput
- Surface Convergence → Focus areas

#### Capping → Blockers
- 700 mb Temp → Organizational inertia
- CINH → Approval bottlenecks

### Winter Storm Analysis (Crisis Mode)

When organization is under stress:

| Indicator | Org Equivalent |
|-----------|----------------|
| Temperature Profile | Cash runway |
| Moisture | Resource availability |
| Lift | External pressure |

### Mesoscale Analysis (Detailed View)

| NWP Source | Org Equivalent |
|------------|----------------|
| SPC Mesoanalysis | Beads detail view |
| Mesoscale Discussion | Slack/async comms |
| Watch/Warning | Incidents, P1 alerts |
| Convective Outlook | Sprint forecast |

## OWF Generation

### Synoptic Time

Current organizational state snapshot:

```bash
# Generate synoptic analysis
./scripts/quality-gate.sh
./scripts/markov-blanket.sh
cat .beads/open.yaml | head -50
cat projects/decision-queue.md | head -30
```

### Model Output Statistics (MOS)

Post-processing to improve raw forecasts:

| MOS Element | Org Equivalent |
|-------------|----------------|
| Temperature bias | Estimation bias (over/under) |
| PoP calibration | Probability calibration |
| Wind correction | Velocity adjustment |

### Forecast Products

Generate organizational weather forecast:

```yaml
# OWF Output
synoptic_time: <current DTG>
valid_through: <+10 days>

panels:
  surface:
    gate: PASSING|FAILING
    blockers: <count>
  upper_flow:
    sprint: <current>
    velocity: <beads/week>
  resources:
    budget: <status>
    capacity: <status>
    cost: <status>
  quality:
    findings: <count>
    o_a_gap: <score>
    confidence: <0-1>

forecast:
  day_1: <events, confidence>
  day_3: <events, confidence>
  day_7: <events, confidence>
  day_10: <events, confidence>

risks:
  - id: <risk_id>
    probability: <0-1>
    impact: HIGH|MED|LOW
    mitigation: <action>
```

## 4-Panel HUD Layout

```
┌─────────────────────────────┬─────────────────────────────┐
│  SURFACE (Gate Status)      │  UPPER FLOW (Sprint)        │
│  🟢 Gateway: PASS           │  Sprint: 26020/MS3          │
│  🟢 Tunnel: PASS            │  Velocity: 4 beads/wk       │
│  🟢 Mesh: PASS              │  Blockers: 1                │
├─────────────────────────────┼─────────────────────────────┤
│  RESOURCES (Blanket)        │  QUALITY (Risk)             │
│  Budget: OK                 │  Findings: 2                │
│  Capacity: OK               │  O-A Gap: LOW               │
│  Cost: YELLOW               │  Confidence: 0.7            │
└─────────────────────────────┴─────────────────────────────┘
```

## Haby Hints → Org Hints Mapping

Key forecasting principles adapted:

| Haby Hint | Org Application |
|-----------|-----------------|
| #60 Model Data Input | Context engineering quality |
| #68 Purpose of Forecast | Actionable predictions |
| #69 Art of Forecasting | Balance data + intuition |
| #70 Forecast Verification | O-A gap tracking |
| #95 Using MOS | Post-process agent output |
| #109 Using Model Progs | Multi-model comparison |

## References

- ADR-008: OWP Architecture
- SPEC-OPR-001: Organization Process Re-engineering
- Haby's Hints: https://www.theweatherprediction.com/habyhints/
- PSU e-wall: https://www.meteo.psu.edu/ewall/ewall.html
- Haby's Map Room: https://www.theweatherprediction.com/maproom/

## Jargon Glossary

| Term | NWP Meaning | Org Meaning |
|------|-------------|-------------|
| Synoptic | Large-scale snapshot | Org-wide state |
| Mesoscale | Regional detail | Team/project level |
| OA | Objective Analysis | LLM-generated forecast |
| O-A Gap | Observation minus Analysis | Prediction error |
| MOS | Model Output Statistics | Calibrated predictions |
| CAPE | Convective energy | Backlog pressure |
| Capping | Inversion layer | Blockers |
| Convergence | Air coming together | Focus/alignment |
| Vorticity | Spin/rotation | Decision momentum |
