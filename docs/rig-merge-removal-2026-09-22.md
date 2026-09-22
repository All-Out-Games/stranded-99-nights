# Remove unused rig recipe

Removed `reusable_weapons/anims/reusable-weapons/player/player.merged_spine_rig`. No default player, script, scene, prefab or other decoded bundled asset in published version `6ab20435236e3076fa1ad98e` references it. The runtime previously registered and loaded it despite its unused output. Required rigs and gameplay are unchanged.

Game: `699f6c23af85880d716a1b16` (99 Nights in the Forest 🔦).
Published source SHA-256: `579af345f4e6fdab76ff27ffd98d224b3e158d09139ef4ebed8b8be5ab90c3eb`.
Prepared candidate SHA-256: `70faa4a9bab3781b69ca3aa0d10dfa3d781f34156432b52e63d840c8d78117b4`.

The release candidate was derived from that exact published source archive; all scripts, scenes and remaining cooked asset entries are byte-identical. This avoids republishing unrelated older files from this authoring checkout. Only the recipe entry and related manifest/bundle metadata were removed. Cloud authoritative scene compilation and release verification are recorded in the engine repository's `docs/rig-startup-rollout-2026-09-22.md`. This commit alone is not evidence of production deployment.
