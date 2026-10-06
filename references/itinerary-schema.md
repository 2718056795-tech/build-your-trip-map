# Itinerary data contract

Create UTF-8 JSON. See `example-itinerary.json` for a complete minimal example.

## Root

```json
{
  "title": "Required",
  "subtitle": "Optional",
  "language": "zh-CN",
  "travelWindow": "2026-09-30—2026-10-08",
  "travelers": "2 adults + one 2-year-old",
  "pace": "Balanced",
  "arrival": "Optional text",
  "departure": "Optional text",
  "fixedWindows": ["13:00–14:00 child nap"],
  "totalDistanceKm": 0,
  "days": [],
  "sources": []
}
```

## Day

Required: `id`, `date`, `title`, `color`, `summary`, `stops`.

```json
{
  "id": "D1",
  "date": "9月30日 · 周三",
  "title": "Arrival and easy river walk",
  "theme": "Recovery",
  "color": "#F97316",
  "summary": "Plain-language day strategy.",
  "distanceKm": 27,
  "travelTime": "about 1 hour",
  "stay": "City Centre",
  "napPlan": "13:00–14:00 hotel nap",
  "risk": "Delete the park if arrival is delayed.",
  "geometry": [[-31.94, 115.96], [-31.97, 115.86]],
  "stops": [],
  "schedule": [],
  "sources": []
}
```

`geometry` is optional and uses `[latitude, longitude]`. Without it, the map connects stop coordinates with a simplified line.

## Stop

Required: `name`, `en`, `lat`, `lng`.

```json
{
  "name": "当地语言名称",
  "en": "English Name",
  "lat": -31.95,
  "lng": 115.86,
  "emoji": "🌳",
  "highlight": true,
  "bookable": false,
  "bookingNote": "",
  "bookingUrl": "",
  "optional": false,
  "distanceFromPreviousKm": 12,
  "travelFromPrevious": "about 20 minutes",
  "note": "What to do and why it fits this day.",
  "image": "https://example.com/photo.jpg",
  "imageAlt": "Descriptive alternative text",
  "sourceUrl": "https://official.example.com/place"
}
```

Use `emoji` only for selected landmarks. The builder uses a numbered marker for ordinary stops and adds `🎟️` to bookable markers.

## Schedule item

```json
{
  "time": "09:00–10:30",
  "title": "Local / English activity name",
  "note": "Buffer, child handling, or fallback."
}
```

## Source

```json
{
  "label": "Official operator",
  "url": "https://official.example.com/"
}
```

Prefer sources at day or stop level. Root sources are for trip-wide transport, safety, or weather guidance.
