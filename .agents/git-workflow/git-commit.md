# Commits

Se sigue el estándar [Conventional Commits 1.0.0](https://www.conventionalcommits.org/es/v1.0.0/). La organización de ramas y los merges están en [git-workflow.md](git-workflow.md).

## Formato

```
<tipo>(<ámbito>): <descripción>

<cuerpo opcional>

<pie opcional>
```

### Cabecera

Primera línea, máximo 72 caracteres.

- **`<tipo>`**: obligatorio, en inglés y en minúsculas (ver [Tipos](#tipos)).
- **`(<ámbito>)`**: opcional. Parte del proyecto afectada, en inglés, en minúsculas y con el mismo nombre que en el código: `(aio)`, `(dio)`, `(config)`.
- **`<descripción>`**: en español, empieza en minúscula, sin punto final y con el verbo en presente y tercera persona: `añade`, `corrige`, `actualiza`, `elimina` (no `añadido` ni `añadir`).

### Cuerpo

Solo si hace falta explicar **por qué** se hizo el cambio; el *qué* ya lo muestra el diff. Va separado de la cabecera por una línea en blanco, con líneas de máximo 72 caracteres.

### Pie

Solo se admite `BREAKING CHANGE: <explicación>`, cuando el cambio rompe la compatibilidad. Equivale a añadir `!` tras el tipo o ámbito: `feat(aio)!: cambia el formato de lectura`.

## Tipos

| Tipo | Cuándo |
|---|---|
| `feat` | Funcionalidad nueva |
| `fix` | Corrección de un error |
| `docs` | Solo documentación |
| `style` | Formato del código (espacios, sangría…) sin cambiar su comportamiento |
| `refactor` | Cambio de código que ni añade funcionalidad ni corrige errores |
| `perf` | Mejora de rendimiento |
| `test` | Añade o corrige pruebas |
| `build` | Sistema de compilación o dependencias (Makefile, CMake…) |
| `ci` | Integración continua |
| `chore` | Mantenimiento que no toca el código ni la documentación |
| `revert` | Deshace un commit anterior |

## Tono

Seco y directo: describe el cambio y nada más. Sin emojis, adjetivos ("mejora increíble", "gran refactor") ni relleno.

## Sin rastro de IA

La IA no se atribuye nada en ninguna parte del mensaje (cabecera, cuerpo o pie), aunque la herramienta lo añada por defecto:

- **Autoría**: siempre la identidad configurada en git (`user.name` / `user.email`). No se modifica.
- **Coautoría**: nada de `Co-Authored-By:` ni líneas similares.
- **Texto**: nada de "Generated with…", "Created by…", nombres de modelos o herramientas de IA, enlaces, emojis de robot ni firmas.

## Contenido

- Un commit = un cambio lógico. No mezclar cambios sin relación.
- No subir archivos generados, binarios compilados, secretos ni claves.
- Revisar `git status` y `git diff --staged` antes de cada commit.

## Ejemplos

Correctos:

```
docs: añade guía del flujo de git
fix(aio): corrige offset del canal 2
feat(dio): añade escritura de salidas
refactor(config): elimina configuración de Modbus sin uso
feat(aio)!: cambia las unidades de lectura a mV
```

Incorrectos:

```
añade guía del flujo de git             ← sin tipo
Docs: Añade guía del flujo de git       ← tipo y descripción en mayúscula
fix: corrige bug.                       ← vago, con punto final
feat(AIO): añadida lectura              ← ámbito en mayúscula, participio
feat: ✨ nueva función increíble         ← emoji y tono
docs: add git workflow guide            ← descripción en inglés
fix: actualiza archivo (hecho con IA)   ← mención a IA
```

Incorrecto, con rastro de IA en el pie:

```
feat(dio): añade lectura de entradas

Co-Authored-By: <asistente de IA> <...>     ← coautoría de IA
🤖 Generated with <herramienta de IA>       ← firma de herramienta
```
