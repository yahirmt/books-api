# Books API

API de libros construida con [Hono](https://hono.dev/) y [Bun](https://bun.sh/). PRUEBAS de 3.3.4

## 🚀 Inicio Rápido

### Instalación

```sh
bun install
```

### Desarrollo

```sh
bun run dev
```

Abre http://localhost:3000

### Docker

```sh
# Desarrollo con servicios completos (PostgreSQL, Redis, etc.)
bun run docker:dev

# Producción
docker pull ghcr.io/yahirmt/books-api:latest
docker run -p 3000:3000 ghcr.io/yahirmt/books-api:latest
```

## 📦 Releases Automáticos

Este proyecto usa **Conventional Commits** para generar releases automáticamente.

**✅ Husky configurado:** Los commits se validan automáticamente antes de aceptarlos.

### Cómo contribuir

```bash
# Nueva funcionalidad
git commit -m "feat: add book search endpoint"

# Corrección de bug
git commit -m "fix: resolve authentication error"

# Breaking change
git commit -m "feat!: redesign API endpoints"
```

**Validación automática:** Si el formato es incorrecto, el commit será rechazado con un mensaje de error claro.

Al hacer push a `main`, Release Please creará automáticamente un PR con:
- Nueva versión calculada
- CHANGELOG actualizado
- Release notes

**📚 Lee más:**
- [RELEASES.md](RELEASES.md) - Sistema de releases automáticos
- [CONTRIBUTING.md](CONTRIBUTING.md) - Guía completa de contribución
- [.github/COMMIT_CONVENTION.md](.github/COMMIT_CONVENTION.md) - Referencia rápida

## 🐳 Docker & CI/CD

- **Desarrollo:** [docker-compose.yml](docker-compose.yml) con PostgreSQL, Redis, Adminer
- **Producción:** [Dockerfile](Dockerfile) multi-stage optimizado
- **CI/CD:** GitHub Actions con releases automáticos
- **Registry:** GitHub Container Registry (GHCR)

**📚 Documentación:**
- [README.Docker.md](README.Docker.md) - Guía de Docker
- [DEPLOYMENT.md](DEPLOYMENT.md) - Guía de despliegue
- [.github/workflows/README.md](.github/workflows/README.md) - Workflows CI/CD

## 🛠️ Scripts Disponibles

```bash
# Desarrollo
bun run dev                    # Inicia servidor con hot-reload

# Docker - Desarrollo
bun run docker:dev             # Inicia stack completo
bun run docker:dev:build       # Rebuild e inicia
bun run docker:down            # Detiene servicios
bun run docker:logs            # Ver logs de la API

# Docker - Producción
bun run docker:prod:build      # Build imagen de producción
bun run docker:prod:run        # Ejecuta imagen de producción
```

## 📂 Estructura del Proyecto

```
books-api/
├── src/
│   └── index.ts              # Punto de entrada
├── .github/
│   ├── workflows/            # GitHub Actions
│   │   ├── auto-release.yml  # Releases automáticos
│   │   ├── ci.yml            # Tests y validación
│   │   └── docker-build.yml  # Build de imágenes
│   └── COMMIT_CONVENTION.md  # Referencia rápida
├── init-db/                  # Scripts de inicialización de DB
├── Dockerfile                # Imagen de producción
├── Dockerfile.dev            # Imagen de desarrollo
├── docker-compose.yml        # Stack de desarrollo
└── release-please-config.json # Configuración de releases
```

## 🔧 Tecnologías

- **Runtime:** Bun
- **Framework:** Hono
- **Base de datos:** PostgreSQL
- **Caché:** Redis
- **Containerización:** Docker
- **CI/CD:** GitHub Actions
- **Registry:** GitHub Container Registry

## 📖 Documentación

| Archivo | Descripción |
|---------|-------------|
| [RELEASES.md](RELEASES.md) | Sistema de releases automáticos |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Guía de contribución completa |
| [README.Docker.md](README.Docker.md) | Guía de Docker |
| [DEPLOYMENT.md](DEPLOYMENT.md) | Guía de despliegue |
| [CHANGELOG.md](CHANGELOG.md) | Historial de cambios |

## 📄 Licencia

MIT
