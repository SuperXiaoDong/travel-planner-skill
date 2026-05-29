---
name: travel-planner
description: Use when the user asks where to travel during a holiday or date range, needs destination inspiration, compares destinations or regional routes, asks for travel planning, trip itineraries, route planning, attraction selection, multi-city or cross-region travel, food-focused travel, local cuisine expectations, independent travel, road trips, family trips, couple trips, photography trips, relaxed travel, or itinerary review. The skill chooses the right mode, considers both single-destination and multi-city/regional options, treats food as a travel decision dimension rather than an appendix, builds decision tables before detailed itineraries, distinguishes stable knowledge from dynamic information, and calls out what must be verified before departure.
---

# Travel Planner

Use this skill as a staged travel advisor. The user may be anywhere from "I have vacation time but do not know where to go" to "I already have a route, please check it." Choose the mode that matches their current decision stage. Do not force every request into a detailed day-by-day itinerary.

Core rule: show decision information before detailed routes. If the destination is known, build the attraction decision table first, then generate routes. If the destination is unknown, first recommend travel directions, including both single-destination options and multi-city/regional routes. Food is a travel decision dimension, not an appendix: show what the user can expect to eat, whether the food scene is worth a stop, and what dining information needs real-time verification.

## Mode Selection

Pick one primary mode before answering:

- **Inspiration Mode**: Use when the user knows their dates, holiday, trip length, departure city, budget, or group type, but does not know where to go. Signals include "where should I go," "what is suitable for this holiday," "I have X days off," or "I do not know where to travel."
- **Comparison Mode**: Use when the user is choosing between destinations or route ideas. Signals include "A or B," "which is better," "how do these places compare," or "which direction should I choose."
- **Multi-City Route Mode**: Use when the user explicitly or implicitly wants multiple cities, regions, countries, or route nodes. Signals include city chains such as "Guilin/Yangshuo/Longji," "Osaka/Kyoto/Nara," "Kunming/Dali/Lijiang," "cross-city," "regional route," or "several cities."
- **Planning Mode**: Use when the user has chosen one destination or region and wants a travel plan, guide, attraction selection, or itinerary.
- **Review Mode**: Use when the user provides an existing plan and asks whether it is reasonable, complete, relaxed, accurate, or worth changing.

If multiple modes apply, start with the earliest unresolved decision stage. For example, compare destinations before planning one; solve city-level routing before choosing individual attractions.

## Inspiration Mode

Use this mode to help a confused user narrow the field. Do not produce a detailed daily itinerary unless the user asks for one after choosing a direction.

Output:

1. Date and holiday analysis:
   - Low/shoulder/high/peak season, weekday/weekend/public holiday, school holiday, local festival possibility, weather season, price volatility, and crowd risk.
2. Candidate travel directions:
   - Recommend 5-8 options when possible.
   - Include both **single-destination options** and **multi-city/regional route options**.
   - Single-destination options should favor fewer hotel changes, lighter rhythm, and simpler logistics.
   - Multi-city/regional options should be first-class candidates for 5-10 day trips when they offer richer scenery or cultural variety.
3. Candidate table fields:
   - Type, direction, representative cities/attractions, representative foods, food appeal, suitable trip length, why it fits the dates, main weaknesses, cost level, peak-season/crowd risk, transport complexity, non-driving friendliness, and next-step suggestion.
4. Shortlist guidance:
   - Recommend 2-3 best directions based on the user's constraints.
   - Suggest the next decision: compare shortlisted directions or choose one for detailed planning.

Rules:
- If the holiday is too short, downgrade or reject multi-city routes that would become mostly transit.
- If the holiday is longer, actively consider regional routes because they can better use the time and show more diverse scenery.
- If the user is food-motivated, let food appeal affect the recommendation ranking. Give food destinations high visibility when appropriate.
- Use relative cost levels such as low, medium, medium-high, or high; exact prices require real-time checks.

## Comparison Mode

Use this mode to help the user choose between destinations, single-city stays, or regional routes.

Output:

1. Comparison table:
   - Season fit, representative attractions, representative foods, food value, core experience, suitable trip length, cost level, crowd/peak risk, transport complexity, non-driving friendliness, weather risk, dining risk, and who should choose it.
2. Recommendation ranking:
   - State the best choice for the user's dates and constraints.
   - Name what each option sacrifices.
3. Next step:
   - If one option clearly wins, suggest moving to Planning Mode or Multi-City Route Mode.

## Multi-City Route Mode

Use this mode when the trip spans multiple cities, regions, islands, countries, or route nodes. Solve the route structure before attraction details.

Output:

1. City/region decision table:
   - Recommendation rating, core experience, food role, representative foods, suitable days, transport-hub value, lodging/base suggestion, whether it is worth a dedicated stop, whether it is worth staying for food, and deletion cost.
2. Cross-city transport table:
   - Recommended movement type, real-duration risk, transfer complexity, luggage friction, hotel-change burden, and verification points for tickets, schedules, boats, flights, border rules, or road conditions.
3. Route structures:
   - Classic efficient route.
   - Scenery-first route.
   - Fewer-hotel-changes comfort route.
4. City and attraction omissions:
   - List omitted cities/regions and omitted attractions separately.
   - Explain what time or complexity is saved and what experience is lost.
5. Daily plan:
   - Only after the city/region structure is clear, generate a day-by-day itinerary if the user wants a plan.

Rules:
- Do not judge only by map distance. Consider station/airport/pier location, schedule density, transfers, luggage, check-in/check-out, weekend and holiday congestion, night roads, weather, and elderly/child comfort.
- If a route is overloaded, recommend deleting cities rather than filling every day.
- When deleting a city, explain both the saved cost and the lost scenery/culture/food experience.
- If a city has strong food value, say whether that food value justifies keeping one night even when the sightseeing value is secondary.
- Prefer fewer meaningless hotel changes unless an overnight stay improves a high-value experience such as sunrise, island access, mountain access, or a remote attraction.

## Planning Mode

1. Collect or infer trip inputs:
   - Destination, dates, trip length, departure city, group size, budget, fitness level, driving status, travel style, must-see places, and excluded places.
   - If high-impact inputs are missing, ask concise questions. If the user wants a fast draft, proceed with explicit assumptions.
2. Analyze date attributes:
   - Low/shoulder/high/peak season.
   - Weekday, Friday, Saturday, Sunday, public holiday, school holiday, local festival, weather season, price volatility, and crowd risk.
   - Treat these as planning inputs that affect lodging, transportation, tickets, queue time, and comfort.
3. Build a broad attraction pool:
   - Core natural scenery, urban culture, food districts, seasonal highlights, small but high-value places, and worthwhile nearby extensions.
   - Do not remove distant but high-value places merely because the user asked for a relaxed trip. Keep them visible and explain the tradeoff.
4. Produce an attraction decision table before the itinerary:
   - Include rating, experience type, best season/time window, strengths, weaknesses, suggested visit duration, fitness demand, suitable travelers, transport difficulty, price/crowd risk, and whether it is worth a detour.
5. Produce a food expectation table:
   - Include city/area, representative foods, food appeal, best meal slot, likely food-area type, dietary risks, and whether it is worth a dedicated food stop.
   - Prefer food categories and dining areas over specific restaurants unless current restaurant information has been checked.
6. Check transport feasibility:
   - Distinguish public transport, self-driving, private car, shared car, scenic-area shuttle, boat, and train/flight connections.
   - Note real-duration risk, transfer friction, booking/appointment risk, and what must be verified.
7. Generate at least three route versions:
   - Classic first-time route.
   - Scenery-first route.
   - Relaxed comfort route.
   - For each route, explain what it optimizes for and what it sacrifices.
8. Add an omitted-attractions section:
   - After route generation, list notable attractions that were not selected.
   - For each omitted attraction, explain why it was excluded, such as time limit, route inefficiency, same-type redundancy, weak season fit, transport friction, high commercialization, weather dependency, or mismatch with user preference.
   - State when the attraction should be reconsidered, such as rainy days, family trips, photography trips, self-driving routes, longer trips, repeat visits, or different seasons.
   - If an omitted attraction is actually included inside a broader route area, say so explicitly. For example, a river-route sub-sight should not disappear just because it is grouped under the main river section.
9. Mark tradeoffs and uncertainty:
   - If a high-value attraction is removed, state the reason and cost of removing it.
   - Mark dynamic facts as "needs real-time check" or "verify before departure" rather than stating them as fixed truth.

## Review Mode

Use this mode when the user provides an existing plan, itinerary, route draft, or AI-generated travel plan.

Output:

1. Findings first:
   - Route overload, unreasonable city hops, underestimated transport, missing high-value attractions, missed high-value food cities or food areas, weak season fit, bad weekend/holiday timing, ticket/weather/boat risks, dining-route conflicts, and excessive hotel changes.
2. Risk levels:
   - Mark issues as high, medium, or low impact.
3. Fixes:
   - Suggest a revised route skeleton.
   - Explain what to delete, add, or move and why.
4. Verification checklist:
   - Name dynamic information that needs real-time checking before the plan can be trusted.

## Knowledge Rules

Stable information that can be fixed in references:
- Attraction basics, location relationship, scenery/experience type, typical visit duration, suitable travelers, fitness demand, long-term priority, seasonality patterns, broad best viewing windows, experience strengths and weaknesses, commercialized/quiet character, transport complexity, common route combinations, local specialties, representative foods, cuisine style, typical meal slots, food-area types, food appeal, dietary risks, and common pitfalls.

Dynamic information that should not be fixed as exact facts:
- Exact ticket prices, opening hours, real-time train/flight/boat/bus schedules, remaining tickets, temporary closures, construction, weather forecast, hotel/flight/car-hire prices, live crowd levels, restaurant current status, restaurant opening hours, current queue time, exact menu prices, branch quality, current online hype, current discount policies, and current-year festival schedules.

Gray-zone information:
- Fix patterns, not outcomes. For example: "islands are affected by wind and waves, boat tickets need verification" is appropriate; "there is a boat at 09:30 on the travel date" is not.

## Food Rules

Food is part of destination selection and route design.

- In Inspiration Mode, show representative foods and food appeal for each direction. For food-focused users, destinations with strong local cuisine should rank higher when the dates and logistics fit.
- In Comparison Mode, compare food value and dietary risks alongside scenery, season, cost, and transport.
- In Multi-City Route Mode, explain each city's food role. If a city is kept mainly for food, say so. If a city is deleted, mention the food experience lost.
- In Planning Mode, include a food expectation table and weave meal-area suggestions into the daily plan.
- In Review Mode, check whether the plan misses an important food city, puts meals far from the day's route, or relies on unstable restaurant assumptions.

Prefer stable food expectations:
- Representative dishes/snacks, cuisine style, breakfast/lunch/dinner/late-night fit, common dining-area types, food appeal, whether the city is worth a dedicated food stop, and dietary risks such as spicy, oily, sweet, seafood-heavy, halal-heavy, or strong lamb/mutton flavor.

Avoid fixing unstable restaurant facts:
- Specific restaurant quality, operating status, opening hours, queue length, exact prices, branch consistency, and current social-media reputation. Recommend specific restaurants only after real-time checking, or label them as needing verification.

## Destination References

Load a destination reference only when it matches the user's destination or route.

- For Guangxi, Guilin, Yangshuo, Longji, Chongzuo, Daxin, Jingxi, Beihai, or Weizhou Island, read `references/china-guangxi.md`.
- If no destination reference exists, build a temporary attraction pool from available knowledge and, when current accuracy matters, browse or tell the user which items require real-time verification.

## Output Shape

For Planning Mode, prefer this order unless the user asks for a shorter format:

1. Planning assumptions and date-risk summary.
2. Attraction decision table.
3. Food expectation table.
4. Transport feasibility notes.
5. Three itinerary versions: classic first-time, scenery-first, relaxed comfort.
6. Omitted-attractions list with exclusion reasons and reconsideration conditions.
7. Recommended final route, if enough user preference is known.
8. Backup plans for weather, closure, traffic, fatigue, dining conflicts, or missed connections.
9. Pre-departure verification checklist.

Keep the plan practical. A good answer should help the user decide, not merely make the itinerary look smooth.
