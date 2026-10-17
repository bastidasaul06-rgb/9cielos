# Nota sobre esta copia de la skill nvgt-dev

Origen: https://github.com/anhlocvu/nvgt-dev-skill (clonada el 2026-10-17).

Esta copia es **funcionalmente completa para desarrollo**, pero se omitieron los
binarios pesados del repositorio original para mantener el repo ligero
(320 MB -> 39 MB). La estructura de directorios se conserva intacta.

## Omitido (solo binarios/derivados, no fuentes)
- `*.dll`, `*.exe`, `*.so`, `*.dylib`, `*.lib`, `*.a`, `*.pdb`
- `*.zip`, `*.7z` (paquetes ya compilados de los juegos de ejemplo)
- `*.usr` (2015 ficheros de partidas guardadas de usuarios reales de "ek src 0.30")
- `*.log` (logs de ejecución)
- Directorios `lib/` y `logs/` que solo contenían lo anterior (se recrearon vacíos)

## Conservado (todo lo que importa para escribir código)
- `nvgt-dev/SKILL.md` — directivas de la skill
- `nvgt-dev/scripts/` — nvgt_researcher.py, asset_manager.py
- `references/API/` — 292 volcados de API generados desde el motor (fuente de verdad)
- `references/nvgt_src/` — código fuente C++ de NVGT 0.90.0-dev + documentación oficial (`doc/src`, 476 ficheros)
- `references/main_dock.md`, `BGT dock.md`, `nvgt_api_reference.md`, `tutorial.md`, etc.
- `references/example_game/` — fuentes `.nvgt` completas de Ultra World, Rotu, Bloodbath, tm, ek, Rhythm Rage
- `references/resources/` — king_audio_engine y recursos de comunidad

## Restaurar los binarios originales
```bash
git clone https://github.com/anhlocvu/nvgt-dev-skill.git
```

## Seguridad
Se redactó una **clave de API de OpenAI real y filtrada** que venía incrustada en el
código del juego de ejemplo de terceros `ek src 0.30/eraserver/server.nvgt` (y su copia
`server - Kopya.nvgt`). GitHub Push Protection bloqueó el push por ese motivo. La clave
fue sustituida por `REDACTED_LEAKED_KEY_REMOVED_BY_ARENA` y el commit se reescribió para
que el secreto no quede en el historial. No afecta a nada útil: era credencial ajena al
proyecto y ese juego de ejemplo solo se conserva como referencia de arquitectura.

Nota: `example_game/rotu/client/decryptkey.txt` contiene la clave AES pública con la que
ese ejemplo cifra su pack de sonidos. Se conserva deliberadamente porque documenta el
sistema de packs/`asset_decryptor` de NVGT.
