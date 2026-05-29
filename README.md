# Travel Planner Skill

Version: 1.0.0

Travel Planner is a Codex skill for staged travel planning. It helps users move from "I have vacation time but do not know where to go" to a practical itinerary, while keeping destination choice, seasonality, transport, food, and tradeoffs visible.

## What It Does

- Recommends travel directions for a date range or holiday.
- Compares destinations and regional routes.
- Plans single-destination and multi-city trips.
- Reviews existing itineraries for overloaded routes, weak timing, missing high-value places, and transport risks.
- Treats food as a decision dimension, not an appendix.
- Separates stable travel knowledge from dynamic information that must be checked before departure.

## Modes

The skill chooses one primary mode based on the user's current stage:

| Mode | Use When | Main Output |
| --- | --- | --- |
| Inspiration Mode | The user knows the holiday/date range but not the destination | Candidate directions, including single-destination and multi-city/regional options |
| Comparison Mode | The user is choosing between destinations or route ideas | Comparison table and recommendation ranking |
| Multi-City Route Mode | The trip spans multiple cities, regions, islands, or countries | City/region decision table, cross-city transport table, route structures |
| Planning Mode | The user has chosen a destination or region | Attraction table, food expectation table, transport notes, route options |
| Review Mode | The user already has a plan | Findings, risk levels, fixes, and verification checklist |

## Installation

Copy the `travel-planner/` folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R travel-planner ~/.codex/skills/
```

Then start a new Codex conversation or reference the skill directly:

```text
[$travel-planner](~/.codex/skills/travel-planner/SKILL.md) 我是吃货，6月想出去玩7天，有什么推荐？
```

## Example Prompts

```text
6月8日到6月14日出去旅游，有什么建议？
```

```text
我是吃货，6月想出去玩7天，有什么推荐？
```

```text
广西和贵州哪个更适合7天自由行？
```

```text
帮我做广西7天自由行，不自驾，想看最美的自然风景，也想吃当地特色。
```

```text
帮我看看这个广西行程合理吗？有没有漏掉重要景点或交通低估？
```

## Included Reference

Version 1.0 includes one destination reference:

- `travel-planner/references/china-guangxi.md`

This reference covers Guangxi planning across Guilin/Yangshuo, Longji, Chongzuo/Daxin, Jingxi, Beihai/Weizhou Island, Nanning, and Liuzhou.

Other destinations can still be planned through the generic workflow, but dynamic information should be checked carefully.

## Dynamic Information Policy

The skill does not treat the following as fixed truth:

- Ticket prices
- Opening hours
- Train, flight, bus, boat, or shuttle schedules
- Remaining tickets
- Temporary closures
- Weather forecasts
- Hotel, flight, car-hire, and restaurant prices
- Restaurant opening status, queue time, or current online reputation
- Current-year festival schedules or local policy changes

For these, the skill should either browse current sources or mark them as needing real-time verification.

## Version 1.0 Scope

Included:

- Multi-stage travel planning workflow
- Single-destination and multi-city route handling
- Food as a core planning dimension
- Omitted-attractions and omitted-cities explanations
- Guangxi reference sample

Not included yet:

- Separate output templates
- Trip retrospective and feedback loop
- Additional destination references
- Automated ticket, hotel, or weather integrations
