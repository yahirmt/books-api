# Sistema de Releases Automáticos

Este proyecto usa **Release Please** para generar releases automáticamente basándose en los mensajes de commit chart 3.3.5.

## 🚀 Cómo funciona

### 1. Usa Conventional Commits

Cuando hagas commits, usa el formato de Conventional Commits:

```bash
# Nueva funcionalidad (incrementa versión MINOR)
git commit -m "feat: add book recommendation engine"

# Corrección de bug (incrementa versión PATCH)
git commit -m "fix: resolve duplicate ISBN validation"

# Breaking change (incrementa versión MAJOR)
git commit -m "feat!: redesign REST API to GraphQL"
```

### 2. Push a main

```bash
git push origin main
```

### 3. Release Please crea un PR automáticamente

El bot analizará tus commits y:
- Calculará la nueva versión (ej: `1.2.3` → `1.3.0`)
- Generará el CHANGELOG.md con todos los cambios
- Actualizará package.json con la nueva versión
- Creará/actualizará un PR con título: `chore(main): release X.Y.Z`

### 4. Revisa y mergea el PR

Revisa el PR de Release Please:
- ✅ Verifica que la versión sea correcta
- ✅ Revisa el CHANGELOG generado
- ✅ Mergea cuando estés listo

### 5. Release automático

Al mergear el PR, automáticamente se:
- ✅ Crea un GitHub Release
- ✅ Genera un tag (ej: `v1.3.0`)
- 🚀 Publica imágenes Docker:
  - `ghcr.io/yahirmt/books-api:1.3.0`
  - `ghcr.io/yahirmt/books-api:latest`
- 🔒 Genera attestation de provenance

## 📋 Tipos de commits

| Tipo | Incrementa | Ejemplo | Nueva versión |
|------|------------|---------|---------------|
| `feat:` | MINOR | `feat: add search` | 3.3.5 → 1.1.0 |
| `fix:` | PATCH | `fix: resolve bug` | 3.3.5 → 1.0.1 |
| `perf:` | PATCH | `perf: optimize db` | 3.3.5 → 1.0.1 |
| `feat!:` | MAJOR | `feat!: new API` | 3.3.5 → 2.0.0 |
| `docs:` | - | `docs: update` | No release |
| `chore:` | - | `chore: deps` | No release |

## 🎯 Ejemplos de uso

### Añadir una nueva funcionalidad

```bash
git add .
git commit -m "feat: add pagination to books endpoint

Add limit and offset parameters to /api/books
to support pagination in the client app.

Closes #42"
git push origin main
```

**Resultado:** Versión MINOR incrementada (1.2.0 → 1.3.0)

### Corregir un bug

```bash
git add .
git commit -m "fix: resolve CORS error in production

Add missing CORS headers for production environment.
Fixes issue where frontend couldn't connect to API.

Fixes #55"
git push origin main
```

**Resultado:** Versión PATCH incrementada (1.2.0 → 1.2.1)

### Hacer un breaking change

```bash
git add .
git commit -m "feat!: migrate from REST to GraphQL

BREAKING CHANGE: All REST endpoints have been removed
in favor of a single GraphQL endpoint at /graphql.

Migration guide: docs/migration-to-graphql.md"
git push origin main
```

**Resultado:** Versión MAJOR incrementada (1.2.0 → 2.0.0)

### Multiple commits

```bash
git commit -m "feat: add user authentication"
git commit -m "feat: add user profile endpoint"
git commit -m "fix: resolve login bug"
git commit -m "docs: update API documentation"
git push origin main
```

**Resultado:** Versión MINOR incrementada (1.2.0 → 1.3.0)
- El changelog incluirá todas las features y fixes
- `docs:` no afecta la versión

## 🔄 Flujo completo

```
┌─────────────────────────────────────────────────┐
│ 1. Developer commits usando Conventional       │
│    git commit -m "feat: add feature"           │
│    git push origin main                        │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 2. GitHub Actions ejecuta auto-release.yml     │
│    Release Please analiza commits              │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 3. Release Please abre/actualiza PR            │
│    Título: "chore(main): release 1.3.0"        │
│    - Actualiza CHANGELOG.md                    │
│    - Actualiza package.json version            │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 4. Developer revisa y mergea PR                │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 5. GitHub Actions auto-release.yml             │
│    - Crea GitHub Release v1.3.0                │
│    - Crea tag v1.3.0                           │
│    - Build y push Docker images                │
│    - Genera attestation                        │
└─────────────────────────────────────────────────┘
```

## ⚙️ Configuración

El sistema está configurado mediante:

- **`.github/workflows/auto-release.yml`**: Workflow principal
- **`release-please-config.json`**: Configuración de Release Please
- **`.release-please-manifest.json`**: Versión actual del proyecto
- **`.commitlintrc.json`**: Validación de commits (opcional)

## 📚 Recursos

- [Guía completa de contribución](CONTRIBUTING.md) - Aprende más sobre Conventional Commits
- [GitHub Workflows README](.github/workflows/README.md) - Documentación de workflows
- [Release Please](https://github.com/googleapis/release-please)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)

## ❓ Preguntas Frecuentes

### ¿Qué pasa si hago un commit sin seguir el formato?

El commit no generará un release. El PR de Release Please no se creará o actualizará hasta que haya commits válidos.

### ¿Puedo hacer múltiples releases?

Sí, cada vez que merges un PR de Release Please, se crea un nuevo release. Los commits subsecuentes generarán un nuevo PR.

### ¿Cómo cancelo un release?

Simplemente cierra el PR de Release Please sin mergearlo. Puedes hacer más commits y el PR se actualizará con la nueva versión calculada.

### ¿Puedo editar el CHANGELOG antes del release?

Sí, puedes hacer commits adicionales al PR de Release Please para modificar el CHANGELOG.md antes de mergearlo.

### ¿Funciona con branches?

Release Please está configurado solo para la rama `main`. Otros branches no generarán PRs de release.

## 🎓 Tips

1. **Lee el CONTRIBUTING.md** para ejemplos detallados
2. **Usa `git cz`** (Commitizen) para ayuda interactiva con commits
3. **Revisa siempre el PR** antes de mergear
4. **Usa scopes** para mejor organización: `feat(api): add endpoint`
5. **Incluye contexto** en el cuerpo del commit cuando sea necesario
