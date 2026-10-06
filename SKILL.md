---
name: build-family-trip-web
description: 规划并生成可分享的、移动端友好的旅行行程网站：双语地名、每日路线地图、距离、预订提醒、景点 emoji 标记、日程、来源链接和完整文字攻略。当用户要求规划、优化、可视化、发布家庭旅行/自驾游/多城市假期，或把表格、现有攻略变成交互地图与行程网站时使用（travel itinerary / trip map / road trip / itinerary website）。定稿路线前必须先询问日期、人数、节奏、目的地、固定休息时段、交通方式和必去活动。

---

# Build Family Trip Web

Turn a travel brief or an existing guide into a constraint-aware itinerary and two static webpages: an interactive route map and a complete written guide.

## Non-negotiable start: interview first

Do not design the final route immediately. Read [references/intake.md](references/intake.md), identify information already supplied, and ask only the missing questions.

Ask at most three short questions per message. The first round must establish:

1. Exact travel dates and arrival/departure times, airports or stations, traveler count, and children’s ages.
2. Must-visit places, optional interests, places to avoid, and the desired geographic scope.
3. Preferred intensity, acceptable daily driving or transfers, and fixed sleep, nap, meal, mobility, or medical constraints.

Ask a second round only when needed for transport, lodging, budget, booking tolerance, language, imagery, or publishing. Never repeat a question the user already answered.

After the answers, show a compact requirement card containing assumptions, hard constraints, flexible preferences, and unresolved risks. Continue automatically when the remaining assumptions are low-risk. Ask again only when a missing choice would materially change the route.

## Workflow

### 1. Inspect inputs

- Preserve supplied spreadsheets, screenshots, PDFs, links, maps, and older itinerary versions.
- Use the appropriate document or spreadsheet skill when available.
- Extract dates, places, stays, booked items, distances, opening windows, sources, and the user’s prior edits.
- Keep alternate route versions in separate output files unless the user explicitly requests replacement.

### 2. Research current facts

Browse when facts may have changed. Prefer official tourism, park, transport, venue, operator, airport, road authority, and weather sources.

Verify:

- opening days and seasonal availability;
- ticket or reservation requirements and cancellation conditions;
- ferry, train, flight, tour, or shuttle timing;
- child age, stroller, car-seat, accessibility, and minimum-participant rules;
- road, park, weather, wildlife, and daylight constraints;
- realistic transfer time, parking, refueling, and arrival buffers.

Label estimates and uncertainties. Never present historical climate averages as a trip forecast. Recheck volatile details close to departure.

### 3. Build the constraint model

Read [references/planning-rules.md](references/planning-rules.md). Classify each requirement as:

- `hard`: flights, booked stays, child sleep, accessibility, safety, fixed tickets;
- `anchor`: must-do activity or core destination;
- `flexible`: nice-to-have stop, restaurant, beach, photo point;
- `fallback`: indoor, short, weather-safe, or fatigue-safe replacement.

Choose a pace tier with the user. Schedule hard constraints first, then anchors, meals and rest, transfers, and finally optional stops.

For families, treat nap and bedtime as routing inputs. Put suitable uninterrupted driving or passive transport inside the nap window when possible. Do not “solve” fatigue by adding late-night driving.

### 4. Optimize and challenge the route

- Calculate per-leg distance, duration, total daily travel, arrival time, and stay sequence.
- Avoid repeated backtracking and frequent one-night stays.
- Place the longest transfer after food, fuel, toilets, and child preparation.
- Add driver-change and activity breaks on long days.
- Mark unrealistic days explicitly and offer a safer split or removal.
- Keep bookable activities out of arrival-day and departure-day critical paths unless unavoidable.
- For every day, identify one item that can be deleted without breaking the route.

Do not optimize only for kilometers. Balance fatigue, fixed windows, weather exposure, booking risk, parking, and the value of each stop.

### 5. Confirm the route before polishing

Present a concise route table containing:

- date and overnight base;
- route and main anchors;
- estimated travel time and distance;
- fixed rest or nap handling;
- advance bookings;
- the main risk or fallback.

Resolve any materially branching issue, then write the final data.

### 6. Create `itinerary.json`

Follow [references/itinerary-schema.md](references/itinerary-schema.md). Use bilingual names when requested. Every mapped stop needs coordinates; never invent them. Geocode or verify coordinates against a reliable map source.

Mark:

- `highlight: true` and a meaningful `emoji` for selected scenic or family landmarks;
- `bookable: true`, `bookingNote`, and `bookingUrl` for advance reservations;
- optional stops with `optional: true`;
- route geometry when road-accurate coordinates are available.

Keep marker emphasis selective. Routine fuel, hotel, and transfer points should remain ordinary pins.

### 7. Build the website

Run:

```bash
node <skill-dir>/scripts/build_site.mjs <itinerary.json> <output-directory>
node <skill-dir>/scripts/validate_itinerary.mjs <itinerary.json> <output-directory>
```

The builder creates:

- `index.html`: interactive Leaflet route map, day filters, distances, emoji highlights, and ticket badges;
- `itinerary.html`: complete text itinerary, booking checklist, schedule, sources, images, and fallback notes.

The pages are static and suitable for local viewing or static hosting. Network access is required for map tiles and CDN-hosted Leaflet unless the agent vendors those assets.

### 8. Verify the result

Always:

- run the validator and read its output;
- inspect generated HTML for placeholder text or `undefined`;
- render at a phone viewport and a desktop viewport;
- click overview, every day selector, representative popups, page links, and external source links;
- verify marker order, ticket badges, bilingual labels, long text wrapping, map bounds, and image fallbacks;
- separate structural validation from browser and physical-device acceptance.

If visual tooling is available, iterate until the mobile map and written guide are readable without horizontal scrolling.

### 9. Publish only when requested

Publishing is an external state change. Use the requested host and preserve verification files, custom domains, and existing deployment settings. Build and verify locally first, then commit, push, wait for deployment, and fetch the live pages to confirm the new content.

Report the live map URL, text-guide URL, changed files, validation evidence, and remaining booking or weather risks.

## Output quality bar

- Use plain language, precise times, and honest uncertainty.
- Show local language plus English names consistently.
- Keep source links beside the claims or days they support.
- Use Emoji to improve scanning, not decorate every stop.
- Give bookable items a visible `🎟️` treatment on both pages.
- Make daily deletion/fallback choices obvious for tired travelers.
- Preserve route versions and user-owned files.
