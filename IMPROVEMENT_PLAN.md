# Kontour Travel Planner — Improvement Plan

_Maintained daily. Last updated: 2026-02-26._

## Priority Roadmap

### Phase 1: Ground Truth Expansion (Week 1-2)
From **circulus-map** and **all-routes** projects:

- [ ] **Aviation route intelligence** — Import route solver logic from circulus-map (geodesic, rhumb, bezier paths). Add `references/routes.json` with major city pairs, distances, typical fares
- [ ] **OurAirports full dataset** — circulus-map has 1.4M records. Extract the useful subset (large/medium airports with commercial service) → upgrade `airports.json` from 500 to ~3,000 airports with runways, elevation, timezone
- [ ] **Route network data** — From all-routes: airline route maps, alliance hub networks, direct/stopover connections between city pairs
- [ ] **Timetable estimates** — all-routes has estimated schedules and prices. Add `references/flight-estimates.json` with typical frequencies and price ranges per route
- [ ] **ETOPS awareness** — From circulus-map: over-water routing constraints. Add to transport planning for ultra-long-haul trips (useful for "safest route" queries)

### Phase 2: Tool Skills (Week 2-3)
Turn passive reference data into executable tools:

- [ ] **Route calculator script** — `scripts/calc-route.sh` that takes origin/destination → returns distance, typical flight time, airlines operating, price estimate
- [ ] **Multi-city optimizer** — `scripts/optimize-route.sh` that takes a set of cities → returns optimal visit order (TSP-lite using geodesic distances)
- [ ] **Projection-aware map links** — From circulus-map's projection engine: generate beautiful static map images for trip overviews (via circulus-map API)
- [ ] **Airport detail lookup** — `scripts/airport-info.sh <IATA>` → returns full airport info, airlines, nearby airports, ground transport
- [ ] **Season/weather oracle** — `scripts/best-time.sh <destination>` → returns best months, weather summary, crowd levels, price seasonality

### Phase 3: Planning Intelligence (Week 3-4)
Deeper planning methodology:

- [ ] **Multi-city planning model** — Extend 9-dimension model to handle multi-city trips with per-leg tracking
- [ ] **Group planning mode** — Handle conflicting preferences across group members (vote/compromise logic)
- [ ] **Visa & requirements checker** — `references/visa-matrix.json` with passport-destination visa requirements
- [ ] **Cultural briefing** — `references/cultural-notes.json` with etiquette, tipping, dress codes, taboos per destination
- [ ] **Packing list generator** — Weather + activity-aware packing lists with weights for carry-on optimization

### Phase 4: Integration & Distribution (Week 4+)
- [ ] **MCP server mode** — Package as an MCP tool that any agent can call
- [ ] **Claude Code slash command** — `/plan-trip` quick entry point  
- [ ] **OpenClaw heartbeat integration** — Proactive trip monitoring (price alerts, weather changes)
- [ ] **Kontour AI deep link generation** — Generate kontour.ai links with pre-filled trip data

## Daily Maintenance Checklist

- [ ] Check for outdated reference data (airline routes change, prices shift)
- [ ] Review user feedback / GitHub issues
- [ ] Update SKILL.md if methodology improves
- [ ] Verify scripts still work
- [ ] Sync improvements back to clawhub

## Data Sources

| Source | What | Location |
|--------|------|----------|
| circulus-map | OurAirports data, geodesic solver, projections, ETOPS | `/Users/kh/.codex/worktrees/2e0d/circulus-map/` |
| all-routes | Route networks, timetables, airline data, PostGIS queries | `/Users/kh/.codex/worktrees/04d0/all-routes/` |
| kontour-ai | Trip planning app, MCP integration, chat + map UI | `/Users/kh/.codex/worktrees/78ee/kontour-ai/` |
| OurAirports | Open airport database | `circulus-map/data/generated/ourairports-airports.json` |
| OpenFlights | Route and airline data | Via all-routes ingestion worker |

## Key Metrics to Track

- skills.sh install count
- clawhub installs
- GitHub stars
- Reference data freshness (last update date per file)
- Script test pass rate
