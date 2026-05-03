# Project Notes for AI Agents

## Minecraft / NeoForge Source Navigation

Decompiled sources for Minecraft and NeoForge ship inside JAR files
(`build/moddev/artifacts/*.jar` and `~/.gradle/caches/.../neoforge-*-sources.jar`)
and are not directly readable via Read/Grep/Glob.

To extract them as plain `.java` files for searching, run:

```bash
./gradlew extractAllSources
```

This populates `build/moddev/extracted-sources/` with the package tree:

- `net/minecraft/...` — Vanilla Minecraft (with NeoForge patches applied)
- `net/neoforged/...` — NeoForge mod loader (events, registries, capabilities, etc.)

The directory lives under `build/`, so it is gitignored and will be regenerated
after `gradlew clean`. If the directory is missing or stale, re-run the task —
do not guess at vanilla / NeoForge behavior.

### Individual tasks

- `./gradlew extractMcSources` — Minecraft (patched) only
- `./gradlew extractNeoforgeSources` — NeoForge only
- `./gradlew extractAllSources` — both (recommended)

### When to use

When investigating vanilla or NeoForge behavior — for example "how does
`FoodProperties` serialize?" or "what events does NeoForge fire on item use?"
— search `build/moddev/extracted-sources/` first.
