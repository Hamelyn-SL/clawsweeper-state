# ClawSweeper state — Hamelyn

Estado generado por el [ClawSweeper self-hosted de Hamelyn](https://github.com/Hamelyn-SL/clawsweeper)
(fork de [openclaw/clawsweeper](https://github.com/openclaw/clawsweeper)). Esta rama `state` es la
fuente de verdad auditable: cada review, decisión y cierre queda versionado aquí por el bot.

> La rama `main` conserva el renderer del dashboard del upstream (por eso habla de openclaw); no lo
> usamos. Todo lo de Hamelyn vive en esta rama.

## Estructura

- `records/<owner-repo>/items/<n>.md` — una review por issue/PR abierto: frontmatter con
  `decision`, `close_reason`, `confidence`, `action_taken`, y el análisis completo debajo.
- `records/<owner-repo>/closed/<n>.md` — reviews archivadas cuando el item se cierra.
- `results/sweep-status/<owner-repo>.json` — último estado del barrido por repo.
- `results/target-fanout-cursors/` — cursores del barrido programado de toda la org.
- `apply-report.json` — resultado del último apply (cierres aplicados y por qué).

## Cómo leerlo rápido

```bash
# reviews vivas de hamelyn-serverless
ls records/hamelyn-sl-hamelyn-serverless/items/

# propuestas de cierre pendientes
grep -l "^decision: proposed_close" records/*/items/*.md

# quién decidió qué y cuándo
git log --oneline -- records/
```

El digest diario de Slack (L–V 08:30, #github-noty) se genera desde esta rama.
