# Open WebUI Project Structure

**Open WebUI** is an extensible, feature-rich, and user-friendly self-hosted AI platform designed to operate entirely offline. It supports various LLM runners like **Ollama** and **OpenAI-compatible APIs**, with built-in inference engine for RAG.

- **Version**: 0.7.2
- **Backend**: Python 3.11+ with FastAPI
- **Frontend**: SvelteKit (Svelte 5 + TypeScript) with Tailwind CSS
- **License**: Open WebUI License (see LICENSE file)

---

## Table of Contents

- [Root Directory](#root-directory)
- [Backend](#backend)
- [Frontend](#frontend)
- [Static Assets](#static-assets)
- [Configuration](#configuration)
- [Testing](#testing)
- [Documentation](#documentation)
- [Deployment](#deployment)
- [Development](#development)

---

## Root Directory

### Configuration Files

| File | Description |
|------|-------------|
| `pyproject.toml` | Python project configuration, dependencies, and build settings |
| `package.json` | Node.js dependencies, scripts, and project metadata |
| `package-lock.json` | Locked Node.js dependency versions |
| `vite.config.ts` | Vite bundler configuration for frontend build |
| `svelte.config.js` | SvelteKit framework configuration |
| `tailwind.config.js` | Tailwind CSS styling configuration |
| `tsconfig.json` | TypeScript compiler configuration |
| `postcss.config.js` | PostCSS configuration for CSS processing |
| `.eslintrc.cjs` | ESLint linting rules configuration |
| `.prettierrc` | Prettier code formatting configuration |
| `.prettierignore` | Files to exclude from Prettier formatting |
| `.gitignore` | Git version control exclusions |
| `.gitattributes` | Git file handling attributes |
| `.npmrc` | npm configuration settings |
| `.env.example` | Example environment variables template |
| `.env` | Local environment variables (not in git) |
| `.eslintignore` | Files to exclude from ESLint |
| `.dockerignore` | Files to exclude from Docker build |

### Docker Configuration

| File | Description |
|------|-------------|
| `Dockerfile` | Main container image build instructions |
| `docker-compose.yaml` | Standard Docker Compose setup |
| `docker-compose.gpu.yaml` | Docker Compose with GPU support |
| `docker-compose.amdgpu.yaml` | Docker Compose for AMD GPU |
| `docker-compose.data.yaml` | Data-focused deployment |
| `docker-compose.api.yaml` | API-only deployment |
| `docker-compose.otel.yaml` | OpenTelemetry observability |
| `docker-compose.a1111-test.yaml` | AUTOMATIC1111 testing |
| `docker-compose.playwright.yaml` | Playwright testing environment |

### Scripts

| File | Description |
|------|-------------|
| `run.sh` | Shell script to run the application |
| `run-compose.sh` | Docker Compose runner script |
| `run-ollama-docker.sh` | Ollama Docker integration script |
| `hatch_build.py` | Hatch build system hooks |

### Documentation Assets

| File | Description |
|------|-------------|
| `README.md` | Main project documentation |
| `CHANGELOG.md` | Version change history |
| `LICENSE` | Project license |
| `LICENSE_HISTORY` | License change history |
| `CODE_OF_CONDUCT.md` | Community guidelines |
| `TROUBLESHOOTING.md` | Common issues and solutions |
| `banner.png` | Project banner image |
| `demo.png` | Demo screenshot |

---

## Backend

**Location**: `backend/`

The Python backend built with FastAPI, providing REST API endpoints, WebSocket support, database management, and integrations with AI services.

### Main Application (`backend/open_webui/`)

| File | Description |
|------|-------------|
| `__init__.py` | Package initialization with CLI entry points (Typer commands) |
| `__main__.py` | Module entry point for `python -m open_webui` |
| `main.py` | FastAPI application setup, middleware, static files, and router mounting |
| `config.py` | Configuration management, database initialization, and migrations |
| `env.py` | Environment variables, logging configuration, and constants |
| `constants.py` | Error messages, task types, and application enums |
| `functions.py` | Function management utilities and decorators |
| `tasks.py` | Background task management with Redis integration |

### Routers (`backend/open_webui/routers/`)

API endpoint modules organized by feature:

| File | Description |
|------|-------------|
| `auths.py` | Authentication endpoints (login, signup, OAuth, API keys) |
| `users.py` | User management (CRUD, profiles, settings) |
| `chats.py` | Chat conversation management |
| `channels.py` | Channel/room management for group chats |
| `models.py` | AI model management and configuration |
| `ollama.py` | Ollama LLM integration endpoints |
| `openai.py` | OpenAI-compatible API integration |
| `files.py` | File upload, storage, and management |
| `folders.py` | Folder organization for chats and files |
| `knowledge.py` | Knowledge base management |
| `memories.py` | User memory/context management |
| `prompts.py` | Prompt templates management |
| `tools.py` | Tool management and execution |
| `functions.py` | Custom function management |
| `images.py` | Image generation (DALL-E, ComfyUI, etc.) |
| `audio.py` | Audio processing, TTS (Text-to-Speech), STT (Speech-to-Text) |
| `retrieval.py` | RAG (Retrieval Augmented Generation) endpoints |
| `pipelines.py` | Processing pipeline configuration |
| `evaluations.py` | Model evaluation and testing |
| `configs.py` | System configuration endpoints |
| `groups.py` | User groups and permissions |
| `notes.py` | Notes feature management |
| `tasks.py` | Background task management endpoints |
| `utils.py` | Utility endpoints |
| `scim.py` | SCIM 2.0 provisioning protocol |

### Database Models (`backend/open_webui/models/`)

ORM models using SQLAlchemy/Peewee:

| File | Description |
|------|-------------|
| `users.py` | User model |
| `auths.py` | Authentication/session model |
| `chats.py` | Chat conversation model |
| `messages.py` | Chat message model |
| `models.py` | AI model configuration model |
| `files.py` | File metadata model |
| `folders.py` | Folder model |
| `knowledge.py` | Knowledge base model |
| `memories.py` | User memory model |
| `prompts.py` | Prompt template model |
| `tools.py` | Tool definition model |
| `functions.py` | Function definition model |
| `channels.py` | Channel/room model |
| `notes.py` | Note model |
| `groups.py` | User group model |
| `tags.py` | Tag model |
| `feedbacks.py` | User feedback model |
| `oauth_sessions.py` | OAuth session model |

### Utilities (`backend/open_webui/utils/`)

Business logic and helper functions:

| File/Directory | Description |
|----------------|-------------|
| `auth.py` | Authentication utilities (JWT, password hashing) |
| `chat.py` | Chat message processing and formatting |
| `middleware.py` | FastAPI middleware (logging, CORS, etc.) |
| `oauth.py` | OAuth provider integrations (Google, GitHub, etc.) |
| `tools.py` | Tool execution engine |
| `embeddings.py` | Embedding model management |
| `code_interpreter.py` | Code execution and sandboxing |
| `redis.py` | Redis connection and caching utilities |
| `db/` | Database connection and utilities |
| `images/` | Image processing utilities |
| `mcp/` | Model Context Protocol handlers |
| `telemetry/` | Telemetry and analytics collection |

### Retrieval System (`backend/open_webui/retrieval/`)

RAG (Retrieval Augmented Generation) implementation:

| Directory | Description |
|-----------|-------------|
| `loaders/` | Document loaders (PDF, YouTube, web pages, etc.) |
| `vector/` | Vector database abstractions (Chroma, pgvector, etc.) |
| `models/` | Embedding and reranking models |
| `web/` | Web search integrations |
| `utils.py` | Retrieval helper functions |

### WebSocket/Socket (`backend/open_webui/socket/`)

Real-time communication handlers:

- WebSocket connection management
- Real-time chat updates
- Live collaboration features

### Internal (`backend/open_webui/internal/`)

Internal utilities and migrations:

- Database migration scripts
- Internal APIs
- System maintenance tools

### Storage (`backend/open_webui/storage/`)

Storage provider abstractions:

- S3 integration
- Google Cloud Storage
- Azure Blob Storage
- Local filesystem storage

### Built-in Tools (`backend/open_webui/tools/`)

Default tools available to the system:

- Web search tools
- Calculator
- Date/time utilities
- Code execution

### Static (`backend/open_webui/static/`)

Static backend assets:

- Default avatars
- System images
- Fallback resources

### Tests (`backend/open_webui/test/`)

Backend test suite:

- Unit tests
- Integration tests
- Test utilities

---

## Frontend

**Location**: `src/`

The SvelteKit frontend with TypeScript, providing the user interface for chat, admin panels, and workspaces.

### Routes (`src/routes/`)

SvelteKit file-based routing structure:

| Route | Description |
|-------|-------------|
| `(app)/+layout.svelte` | Main application layout wrapper |
| `(app)/+page.svelte` | Default redirect page |
| `(app)/admin/` | Admin panel routes |
| `(app)/admin/+page.svelte` | Admin dashboard |
| `(app)/c/` | Chat routes |
| `(app)/c/[id]/` | Individual chat pages |
| `(app)/channels/` | Channel/room routes |
| `(app)/home/` | Home page |
| `(app)/notes/` | Notes feature routes |
| `(app)/playground/` | Model playground |
| `(app)/workspace/` | User workspace |
| `auth/` | Authentication pages (login, signup) |
| `s/[id]/` | Shared chat pages (public links) |
| `watch/` | Watch mode page |
| `error/` | Error handling pages |

### Components (`src/lib/components/`)

Reusable Svelte components organized by feature:

#### Admin Components (`src/lib/components/admin/`)

- Admin.svelte - Main admin panel
- Settings/ - Settings sub-components
- Users/ - User management UI
- Functions/ - Function management
- Evaluations/ - Evaluation tools

#### Chat Components (`src/lib/components/chat/`)

- Chat.svelte - Main chat interface
- Messages.svelte - Message list display
- MessageInput.svelte - Input field for messages
- Message.svelte - Individual message display
- Placeholder.svelte - Empty state placeholder
- ModelSelector.svelte - Model selection dropdown
- Settings/ - Chat settings
- Messages/ - Message sub-components
- Sidebar/ - Chat sidebar

#### Channel Components (`src/lib/components/channel/`)

- Channel list
- Channel creation
- Channel settings

#### Workspace Components (`src/lib/components/workspace/`)

- Models/ - Model management UI
- Prompts/ - Prompt management
- Tools/ - Tool management
- Knowledge/ - Knowledge base UI

#### Notes Components (`src/lib/components/notes/`)

- Notes editor
- Notes list
- Notes organization

#### Playground Components (`src/lib/components/playground/`)

- Model playground interface
- Testing utilities

#### Layout Components (`src/lib/components/layout/`)

- Sidebar.svelte - Main navigation sidebar
- Navbar.svelte - Top navigation bar
- Drawer.svelte - Slide-out drawer

#### Common Components (`src/lib/components/common/`)

- Buttons, inputs, modals
- Loading spinners
- Toast notifications
- Dropdown menus

#### Icons (`src/lib/components/icons/`)

- Custom SVG icon components

### API Clients (`src/lib/apis/`)

Frontend API wrapper modules matching backend routers:

- `auths/` - Authentication API
- `users/` - User management API
- `chats/` - Chat API
- `channels/` - Channel API
- `models/` - Model API
- `ollama/` - Ollama integration API
- `openai/` - OpenAI API integration
- `files/` - File API
- `folders/` - Folder API
- `knowledge/` - Knowledge base API
- `memories/` - Memory API
- `prompts/` - Prompt API
- `tools/` - Tool API
- `images/` - Image generation API
- `audio/` - Audio API
- `retrieval/` - RAG API
- `configs/` - Configuration API
- `groups/` - Groups API
- `evaluations/` - Evaluation API
- `streaming/` - Streaming response handlers
- `utils/` - Utility API endpoints

### Stores (`src/lib/stores/`)

Svelte stores for global state management:

- `index.ts` - Main store exports
- `user.ts` - Current user state
- `chat.ts` - Chat state
- `models.ts` - Available models
- `config.ts` - Application configuration
- `theme.ts` - Theme settings
- `i18n.ts` - Internationalization state

### Types (`src/lib/types/`)

TypeScript type definitions:

- `index.ts` - Main type exports
- `user.ts` - User-related types
- `chat.ts` - Chat-related types
- `model.ts` - Model-related types
- `file.ts` - File-related types

### Utilities (`src/lib/utils/`)

Frontend helper functions:

- `index.ts` - Main utility exports
- `chat.ts` - Chat formatting utilities
- `date.ts` - Date formatting
- `file.ts` - File handling
- `markdown.ts` - Markdown processing
- `api.ts` - API helper functions

### Constants (`src/lib/constants/`)

Application constants:

- `index.ts` - Main constants
- `messages.ts` - Default messages
- `settings.ts` - Default settings

### Internationalization (`src/lib/i18n/`)

Multi-language support:

- `locales/` - Translation files for each language
- `index.ts` - i18n configuration

### Workers (`src/lib/workers/`)

Web Workers for background processing:

- `pyodide/` - Pyodide Python execution worker
- `markdown/` - Markdown rendering worker

### Pyodide Integration (`src/lib/pyodide/`)

Browser-based Python execution:

- Python code execution in the browser
- Code interpreter integration

### Styles (`src/`)

| File | Description |
|------|-------------|
| `tailwind.css` | Tailwind CSS entry point |
| `app.html` | HTML template |

---

## Static Assets

**Location**: `static/`

Static files served directly:

| File/Directory | Description |
|----------------|-------------|
| `favicon.png` | Website favicon |
| `user.png` | Default user avatar |
| `image-placeholder.png` | Placeholder for images |
| `marker-icon-2x.png` | Map marker icon |
| `robots.txt` | SEO robots configuration |
| `manifest.json` | Web app manifest |

### Static Assets (`static/static/`)

| File | Description |
|------|-------------|
| `favicon.ico` | Browser favicon |
| `favicon.svg` | SVG favicon |
| `favicon.png` | PNG favicon variants |
| `logo.png` | Application logo |
| `splash.png` | App splash screen |
| `splash-dark.png` | Dark mode splash screen |
| `user.png` | User avatar placeholder |
| `apple-touch-icon.png` | iOS home screen icon |
| `web-app-manifest-*.png` | PWA icons |
| `site.webmanifest` | PWA manifest |
| `custom.css` | Custom CSS overrides |
| `loader.js` | Loading script |
| `user-import.csv` | User import template |

### Themes (`static/themes/`)

| File | Description |
|------|-------------|
| `rosepine.css` | Rosé Pine theme |
| `rosepine-dawn.css` | Rosé Pine Dawn theme |

### Pyodide (`static/pyodide/`)

WebAssembly Python runtime and packages:

- Various `.whl` wheel files for Python packages
- Python standard library
- `README.md` - Pyodide setup instructions

---

## Configuration

### Python Dependencies (`pyproject.toml`)

Key dependencies:
- **FastAPI** - Web framework
- **SQLAlchemy** - ORM for database
- **Alembic** - Database migrations
- **LangChain** - LLM integration framework
- **Transformers** - Hugging Face models
- **ChromaDB** - Vector database
- **Redis** - Caching and pub/sub
- **Peewee** - Alternative ORM

Optional dependencies:
- PostgreSQL support (`psycopg2`, `pgvector`)
- Various vector databases (Milvus, Qdrant, etc.)

### Frontend Dependencies (`package.json`)

Key dependencies:
- **SvelteKit** - Framework
- **Svelte 5** - UI library
- **Vite** - Build tool
- **Tailwind CSS** - Styling
- **Tiptap** - Rich text editor
- **Socket.io-client** - Real-time communication
- **Pyodide** - Python in browser
- **Marked** - Markdown rendering
- **Mermaid** - Diagram rendering
- **Chart.js** - Charts
- **Vega-Lite** - Data visualization
- **Yjs** - Collaborative editing

---

## Testing

### E2E Tests (`cypress/`)

End-to-end testing with Cypress:

| File | Description |
|------|-------------|
| `cypress.config.ts` | Cypress configuration |
| `support/e2e.ts` | Test setup and utilities |
| `support/index.d.ts` | Type definitions |
| `e2e/chat.cy.ts` | Chat feature tests |
| `e2e/documents.cy.ts` | Document management tests |
| `e2e/settings.cy.ts` | Settings tests |
| `e2e/registration.cy.ts` | User registration tests |

---

## Documentation

**Location**: `docs/`

Additional documentation:

| File | Description |
|------|-------------|
| `README.md` | Documentation overview |
| `CONTRIBUTING.md` | Contribution guidelines |
| `SECURITY.md` | Security policies |
| `apache.md` | Apache server configuration |

---

## Deployment

### Kubernetes (`kubernetes/`)

Kubernetes deployment manifests:

- Helm charts
- Kustomize configurations
- Raw YAML manifests

### GitHub Actions (`.github/`)

CI/CD workflows:

**Workflows (`.github/workflows/`):**

| File | Description |
|------|-------------|
| `docker-build.yaml` | Docker image build and push |
| `build-release.yml` | Release builds |
| `release-pypi.yml` | PyPI package publishing |
| `deploy-to-hf-spaces.yml` | Hugging Face Spaces deployment |
| `format-backend.yaml` | Backend code formatting |
| `format-build-frontend.yaml` | Frontend formatting and build |
| `lint-backend.disabled` | Backend linting (disabled) |
| `lint-frontend.disabled` | Frontend linting (disabled) |
| `integration-test.disabled` | Integration tests (disabled) |
| `codespell.disabled` | Spell checking (disabled) |

**Pull Request Template:**
- `.github/pull_request_template.md` - PR template

### Build Directory (`build/`)

Frontend build output:

- Compiled SvelteKit application
- Static assets
- `_app/version.json` - Build version info

### Scripts Directory (`scripts/`)

Build and utility scripts:

| File | Description |
|------|-------------|
| `prepare-pyodide.js` | Prepare Pyodide packages |

---

## Key Features

1. **Multi-Model Support**: Ollama, OpenAI, Anthropic, Google GenAI
2. **RAG System**: Document upload, vector search, web search
3. **Tools**: Custom function/tools execution
4. **Real-time**: WebSocket for live updates
5. **Authentication**: OAuth, LDAP, API keys, SSO
6. **Storage**: Multiple vector DBs (Chroma, PostgreSQL/pgvector, Milvus, etc.)
7. **Code Execution**: Pyodide in browser + Jupyter integration
8. **Admin Panel**: User management, system settings
9. **Voice/Video**: Hands-free communication with TTS/STT
10. **Image Generation**: DALL-E, ComfyUI, AUTOMATIC1111
11. **PWA Support**: Progressive Web App for mobile
12. **Collaboration**: Channels and shared chats
13. **Internationalization**: Multi-language support

---

## Development

### Starting the Application

To run Open WebUI locally for development, you need to start both the backend and frontend servers.

#### Prerequisites

- **Node.js** (v18+) and npm installed
- **Python** (3.10+) installed
- Backend dependencies installed in `backend/venv/`

#### 1. Start the Backend Server

Start the FastAPI server:

```bash
conda activate open-webui
python -m uvicorn open_webui.main:app --port 8080 --host 0.0.0.0
```

The backend will be available at `http://localhost:8080`

#### 2. Start the Frontend Dev Server

```bash
npm run dev
```

The frontend will be available at `http://localhost:5173`

#### 3. Access the Application

1. Open your browser to `http://localhost:5173`
2. Click **"Sign up"** to create the first admin account
3. Log in with your credentials
