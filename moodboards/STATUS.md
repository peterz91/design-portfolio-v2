# Project Status — Portfolio Redesign

**Owner:** Peter (peterz91) · **Phase:** 1 of 2 — Moodboards
**Working branch:** `claude/portfolio-redesign-moodboards-absfkt`

## The plan
1. Three B&W moodboard directions (seeded by Joel Tjintjelaar's fine-art photography) → see `DIRECTIONS.md` for full briefs + 24 ready image-generation prompts (8 per direction, aspect ratios noted).
2. Generate images via FLORA (flora.ai) MCP connector → assemble 3 moodboard pages → Peter picks a direction.
3. Phase 2: design + build the actual portfolio from the winning board. New site lives in this repo (`design-portfolio-v2`, currently empty). Old site: peterz91.github.io/design-portfolio (source in repo `peterz91/design-portfolio` — can be added to a session via add_repo for content inventory: name, projects, copy).

## Current blockers
None. **Phase 2 in progress — mockup iteration.** Monolith direction locked; all exploration is image-gen (HTML heroes parked in `explorations/hero/`). Rounds in `explorations/mockups/`: round1 (photographic heroes) → round2-vector (geometric slab heroes, SVG-rebuildable) → round3-ui-objects ("Monolith UI" specimen sheets; light = interaction language: hover lit from above, active glows within, disabled crumbles) → round4-menacing (cosmic-horror ambient: external cold light only, NO glow, eternal lone monoliths, expedition-log captions SPECIMEN I–VIII) → round5-vector-void (same dread ambient but crisp ACTUAL UI elements — true proportions, clean labels, SPECIMEN IX–XVI; Peter's favored trajectory). Mockup model: t2i-gemini-3-pro @2K ($0.18/img), ~$8.4 total spend. NOTE: FLORA execute 502s on large calls — creations usually went through; recover by mapping newest N runs from generations.list in creation order (don't trust time windows — see round-2 mismap).

## Resolved
- **Network egress**: environment switched to Full (took effect live, no restart needed).
- **FLORA MCP connected.** Root cause of earlier failure: `https://flora.ai/mcp` is a marketing page; real endpoint is `https://agents.flora.ai/mcp`. Connected and working (tools: mcp__FLORA_ai__execute / search_docs).
- **All 24 moodboard images generated** (Flux 2 Pro, `t2i-flux-2-pro`, ~$0.036/image, ~$0.87 total) into FLORA project "Portfolio Moodboards" (`prj_ns720ftatypept0e8kagd2xv5d8at5jh`, workspace `ws_qd7ay1men88qjyscfjpbbndhx584t464`). Saved to `moodboards/img/<direction>/`; contact sheets in `moodboards/boards/*.jpg` (built by scratchpad `make_boards.py`, Pillow masonry layout).

## Plan B if connector stays broken
Peter generates the 24 prompts from `DIRECTIONS.md` directly in FLORA's app/canvas and shares outputs (chat upload or into `moodboards/img/<direction>/`); moodboard pages get assembled from those.

## Done so far
- Direction briefs written and pushed (`DIRECTIONS.md`).
- Network unblocked; FLORA connector failure root-caused (wrong URL).
- Old site content pulled from live site into `reference/old-site/` (index.html + script.js). Key facts: **Petar Živković**, "Interface designer", 10 yrs experience, Croatian brands, now focused on end-to-end mobile/web design. Contact peter.zivkovic@gmail.com · x.com/ZivkovicPeter · dribbble.com/pzivkovic · github.com/peterz91. Projects incl.: Uštedi App, STMNT Studios, SkyAccess, Restaurant website (Procida). Old site has a light/dark theme toggle, tabbed project nav, PhotoSwipe gallery, Geologica font.

## Next actions
1. Verify network egress (curl any external site; check `$HTTPS_PROXY/__agentproxy/status` relay failures if blocked).
2. Probe FLORA's OAuth metadata (`/.well-known/oauth-protected-resource`, `/.well-known/oauth-authorization-server` on flora.ai) to pin down the DCR failure; advise Peter.
3. When FLORA connects (tools will appear as mcp__*flora* after enabling the connector on the session): generate all 24 images per DIRECTIONS.md, save under `moodboards/img/<direction>/`, build three static moodboard pages, share for review.
4. Direction locked → phase 2 (portfolio design explorations).
