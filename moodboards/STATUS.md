# Project Status — Portfolio Redesign

**Owner:** Peter (peterz91) · **Phase:** 1 of 2 — Moodboards
**Working branch:** `claude/portfolio-redesign-moodboards-absfkt`

## The plan
1. Three B&W moodboard directions (seeded by Joel Tjintjelaar's fine-art photography) → see `DIRECTIONS.md` for full briefs + 24 ready image-generation prompts (8 per direction, aspect ratios noted).
2. Generate images via FLORA (flora.ai) MCP connector → assemble 3 moodboard pages → Peter picks a direction.
3. Phase 2: design + build the actual portfolio from the winning board. New site lives in this repo (`design-portfolio-v2`, currently empty). Old site: peterz91.github.io/design-portfolio (source in repo `peterz91/design-portfolio` — can be added to a session via add_repo for content inventory: name, projects, copy).

## Current blockers
1. **FLORA MCP connector fails OAuth.** Custom connector URL `https://flora.ai/mcp` added on claude.ai, but Connect fails with: "Couldn't register with FLORA.au's sign-in service… add an OAuth Client ID in the connector settings." Support reference: `ofid_62feed4603f14613`. Dynamic client registration is being refused by FLORA's server. Fix ladder: retry once from desktop → OAuth Client ID from FLORA into connector Advanced settings (callback `https://claude.ai/api/mcp/auth_callback`) → FLORA support with the reference. Note: MCP traffic routes via Anthropic servers, so this is independent of sandbox network policy.
2. **Sandbox network policy was "Trusted"** (package registries + GitHub only) — blocked viewing external sites incl. flora.ai and the old portfolio. Peter is switching the environment's Network access to Full (claude.ai/code → environment selector). GitHub git operations work regardless (separate proxy).

## Plan B if connector stays broken
Peter generates the 24 prompts from `DIRECTIONS.md` directly in FLORA's app/canvas and shares outputs (chat upload or into `moodboards/img/<direction>/`); moodboard pages get assembled from those.

## Done so far
- Direction briefs written and pushed (`DIRECTIONS.md`).
- Diagnosed connector + network issues (above).

## Next actions
1. Verify network egress (curl any external site; check `$HTTPS_PROXY/__agentproxy/status` relay failures if blocked).
2. Probe FLORA's OAuth metadata (`/.well-known/oauth-protected-resource`, `/.well-known/oauth-authorization-server` on flora.ai) to pin down the DCR failure; advise Peter.
3. When FLORA connects (tools will appear as mcp__*flora* after enabling the connector on the session): generate all 24 images per DIRECTIONS.md, save under `moodboards/img/<direction>/`, build three static moodboard pages, share for review.
4. Direction locked → phase 2 (portfolio design explorations).
