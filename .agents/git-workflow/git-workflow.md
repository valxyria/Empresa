# Flujo de git

Organización de ramas e integración de cambios. El formato de los mensajes está en [git-commit.md](git-commit.md).

## Reglas para agentes

- No hacer commits, push ni merges sin petición explícita del usuario.
- No reescribir historial publicado: nada de `push --force`, `rebase` ni `commit --amend` sobre commits ya subidos.
- Ningún rastro de IA en los commits (ver [Sin rastro de IA](git-commit.md#sin-rastro-de-ia)).

## Ramas

```
main      ●──────────────────────●──────────►   releases
           \                    /
develop     ●────●─────────●───●────────────►   desarrollo (siempre funcional)
                  \       /
feature/<nombre>   ●──●──●                      trabajo en curso (puede no funcionar)
```

| Rama | Propósito | Estado de los commits | Sale de | Se integra en |
|---|---|---|---|---|
| `main` | Releases | Cada commit es una versión publicada | — | — |
| `develop` | Desarrollo | Siempre **funcional**: compila, hace lo que debe, sin bugs conocidos y usable en cualquier momento | `main` | `main` |
| `feature/<nombre>` | Una tarea: funcionalidad, corrección, documentación… | Puede **no funcionar** mientras está en curso | `develop` | `develop` |

- `main` y `develop` nunca reciben commits directos, solo merges.
- Cada merge de `develop` en `main` es una release.
- Una `feature/` solo entra en `develop` cuando es funcional y está probada.
- Una rama `feature/` = una tarea. Otra tarea, otra rama.

### Nombres

`feature/<nombre>`, donde `<nombre>` es corto y descriptivo, en español, en minúsculas, sin tildes ni `ñ` y con palabras separadas por guiones.

Ejemplos: `feature/guia-flujo-git`, `feature/lectura-modulo-aio`, `feature/corrige-timeout-dio`.

## Flujo de trabajo

### Empezar una tarea

```bash
git checkout develop
git pull
git checkout -b feature/<nombre>
git push -u origin feature/<nombre>
```

### Trabajar

Commits pequeños en la `feature/` (ver [git-commit.md](git-commit.md)) y `git push` para subirlos.

### Integrar en `develop`

Solo cuando la `feature/` funciona y está probada.

```bash
git checkout develop
git pull
git merge --no-ff feature/<nombre> -m "Integra feature/<nombre> en develop"
git push

# Borrar la rama en local y en remoto
git branch -d feature/<nombre>
git push origin --delete feature/<nombre>
```

### Publicar una release

Solo cuando el contenido de `develop` se quiere publicar.

```bash
git checkout main
git pull
git merge --no-ff develop -m "Integra develop en main"
git push
git checkout develop
```

### Merges

- `--no-ff` crea siempre un commit de merge, para que el historial muestre qué entró y cuándo.
- El mensaje se escribe en español con `-m` (por defecto git lo genera en inglés) y no sigue el formato de [git-commit.md](git-commit.md).
