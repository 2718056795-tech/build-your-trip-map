# Constraint-aware itinerary planning

## Pace tiers

Use these as starting points, then adapt to road conditions and traveler capability.

| Tier | Main anchors | Ordinary transfer | Recovery pattern |
|---|---:|---:|---|
| Relaxed | 1/day | up to about 2 hours | frequent two-night bases |
| Balanced | 1–2/day | up to about 3.5 hours | recovery after long transfer |
| Full | 2–3/day | up to about 5 hours | explicit low-intensity half-day |

Any day above the user’s normal limit is an exception, not the new baseline. Explain the tradeoff and provide a split.

## Scheduling order

1. Arrival, departure, booked stays, and safety constraints.
2. Child sleep, meals, medication, accessibility, and driver-rest windows.
3. Fixed-time tickets, ferries, tours, and seasonal activities.
4. Must-do destinations.
5. Transfers, check-in, parking, fuel, and buffers.
6. Flexible scenery, food, and photo stops.

## Family routing

- Put an uninterrupted compatible drive or train/ferry segment inside a nap window when practical.
- Finish food, toilets, diaper changes, and refueling before the nap segment.
- Do not depend on a child sleeping through frequent stops.
- Avoid fixed-ticket activities immediately after a long drive.
- Add a low-intensity day after an exceptional transfer.
- On non-car days, provide stroller, bus, quiet indoor, or hotel-nap options.
- Keep the final day near the departure corridor.

## Booking classification

Use `bookable: true` when the itinerary materially depends on a reservation, timed entry, limited-capacity tour, ferry, train, permit, or seasonal operator.

For each bookable item record:

- official booking URL;
- recommended booking timing;
- check-in or arrival buffer;
- cancellation/weather policy;
- child, stroller, accessibility, or minimum-age rules;
- fallback if unavailable.

Ordinary on-site admission does not automatically require a ticket badge.

## Risk checks

- Weather and seasonality.
- Road length, road type, fatigue, fuel, and wildlife after dark.
- Parking and entrance location versus the named attraction.
- Border, visa, rental-car, ferry-carriage, park-permit, or insurance restrictions.
- Same-day connections with insufficient buffers.
- Hotel check-in assumptions that are not guaranteed.
- Images without reusable rights or attribution.

## Day acceptance test

A day is ready only when it has:

- a realistic start and finish;
- total transfer time and distance;
- meals and rest;
- fixed-window handling;
- one clear optional deletion;
- booking instructions where required;
- weather/fatigue fallback;
- overnight base or departure endpoint.
