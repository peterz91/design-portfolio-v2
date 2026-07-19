# Project Status — Portfolio Redesign

**Owner:** Peter (peterz91) · **Phase:** 1 of 2 — Moodboards
**Working branch:** `claude/portfolio-redesign-moodboards-absfkt`

## The plan
1. Three B&W moodboard directions (seeded by Joel Tjintjelaar's fine-art photography) → see `DIRECTIONS.md` for full briefs + 24 ready image-generation prompts (8 per direction, aspect ratios noted).
2. Generate images via FLORA (flora.ai) MCP connector → assemble 3 moodboard pages → Peter picks a direction.
3. Phase 2: design + build the actual portfolio from the winning board. New site lives in this repo (`design-portfolio-v2`, currently empty). Old site: peterz91.github.io/design-portfolio (source in repo `peterz91/design-portfolio` — can be added to a session via add_repo for content inventory: name, projects, copy).

## Current blockers
1. **FLORA MCP connector — root cause FOUND, awaiting reconnect.** The originally used URL `https://flora.ai/mcp` is a Framer *marketing page*, not an MCP server — that's why OAuth auto-registration failed ("Couldn't register with FLORA.au's sign-in service", ref `ofid_62feed4603f14613`). The real endpoint is **`https://agents.flora.ai/mcp`** (verified 2026-07-19: proper 401 Bearer challenge, protected-resource metadata, auth-server metadata with live `/register` DCR endpoint, PKCE S256). Fix: delete the broken connector on claude.ai → add custom connector "FLORA" with `https://agents.flora.ai/mcp` → Connect/approve → enable on the session. FLORA dev docs: https://developer.flora.ai/mcp/install/other-clients/

## Resolved
- **Network egress**: environment switched to Full (took effect live, no restart needed). External sites reachable from sandbox.

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
