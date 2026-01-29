# Claude Vue Starter Kit

**Build Laravel apps faster with AI-powered agentic development.**

[![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![Vue.js](https://img.shields.io/badge/Vue.js-3-4FC08D?style=flat-square&logo=vue.js&logoColor=white)](https://vuejs.org)
[![Inertia.js](https://img.shields.io/badge/Inertia.js-2-9553E9?style=flat-square&logo=inertia&logoColor=white)](https://inertiajs.com)
[![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?style=flat-square&logo=php&logoColor=white)](https://php.net)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## What is this?

An opinionated Laravel starter kit fine-tuned for **agentic development with Claude Code**. Instead of writing every line yourself, you collaborate with specialized AI agents that understand Laravel conventions, Vue.js patterns, and testing best practices.

This kit provides:

- **Multi-agent orchestration** — Three specialized agents (backend, UI, QA) that handle different aspects of development
- **Structured workflow** — A 4-phase development cycle (Explore → Plan → Validate → Implement) that ensures quality
- **Domain-specific skills** — Pre-loaded knowledge for Vue 3, Inertia.js v2, Pest testing, and Fortify authentication
- **MCP integrations** — Laravel Boost for app introspection and Playwright for browser testing

Think of it as pair programming where your partner already knows Laravel and Vue inside and out.

---

## Features

- **Pre-configured Claude Code agents**
    - `backend-engineer` — APIs, database, Eloquent, services, authentication, Inertia controllers
    - `ui-engineer` — Vue components, Inertia pages, shadcn-vue, Tailwind, TypeScript
    - `qa-expert` — Test strategy, E2E testing, quality metrics

- **Domain-specific skills** that activate automatically
    - Vue 3 Composition API with `<script setup>`
    - Inertia.js v2 with deferred props, polling, and prefetching
    - Pest 4 testing framework
    - Laravel Fortify authentication
    - Wayfinder for type-safe routes

- **Structured development workflow**
    - Mandatory exploration before implementation
    - Plan approval gates
    - Subagent delegation rules

- **Modern Laravel stack**
    - Laravel 12 with streamlined structure
    - Vue 3 with Composition API and TypeScript
    - Inertia.js v2 for SPA-like navigation
    - Tailwind CSS 4 with CSS-first configuration
    - shadcn-vue (Reka UI) for polished components

- **Ready-to-use authentication**
    - Login, registration, password reset
    - Email verification
    - Two-factor authentication (2FA)
    - Profile management

---

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Laravel | 12.x | PHP framework |
| Vue.js | 3.x | Reactive UI framework |
| Inertia.js | 2.x | SPA-like navigation |
| TypeScript | 5.x | Type-safe JavaScript |
| Tailwind CSS | 4.x | Utility-first CSS |
| shadcn-vue | - | Component library (Reka UI) |
| Pest | 4.x | Testing framework |
| Fortify | 1.x | Authentication backend |
| Wayfinder | 0.x | Type-safe route generation |
| PHP | 8.2+ | Runtime |

---

## Prerequisites

Before you begin, make sure you have:

- **PHP 8.2+** with required extensions
- **Composer** for PHP dependencies
- **Node.js 18+** and npm for frontend assets
- **Claude Code CLI** installed and authenticated
- **SQLite** (default) or MySQL/PostgreSQL

### Install Claude Code

If you haven't already, install Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```

Then authenticate:

```bash
claude login
```

---

## Quick Start

### Option 1: Laravel Installer (Recommended)

```bash
laravel new my-app --using=laravel-agent-kits/claude-vue-starter-kit
```

### Option 2: Composer Create-Project

```bash
composer create-project laravel-agent-kits/claude-vue-starter-kit my-app
cd my-app
```

### Post-Installation

```bash
# Install frontend dependencies
npm install

# Build assets
npm run build

# Start the development server
composer run dev
```

Then open your browser to `http://localhost:8000`.

---

## MCP Server Setup

This starter kit is designed to work with two MCP (Model Context Protocol) servers that supercharge Claude Code's capabilities.

### 1. Laravel Boost (Required)

Laravel Boost gives Claude Code deep insight into your Laravel application — database schemas, routes, configurations, error logs, and version-specific documentation.

#### Installation

```bash
# It's already included as a dev dependency
composer require laravel/boost --dev
```

#### What it provides

| Tool | Purpose |
|------|---------|
| `application-info` | App overview, packages, environment |
| `database-schema` | Table structures and relationships |
| `list-routes` | All registered routes |
| `search-docs` | Version-specific Laravel documentation |
| `tinker` | Execute PHP in app context |
| `last-error` | Recent application errors |
| `browser-logs` | Frontend console output |

#### Configuration

Laravel Boost is auto-configured via the `mcp.json` file in your project root. No additional setup required.

### 2. Playwright MCP (Recommended)

Playwright MCP enables Claude Code to interact with your application in a real browser — taking screenshots, filling forms, clicking buttons, and verifying visual output.

#### Installation

```bash
# Add Playwright MCP to Claude Code
claude mcp add playwright npx @playwright/mcp@latest
```

That's it! Claude Code will handle the rest.

#### What it provides

| Tool | Purpose |
|------|---------|
| `browser_navigate` | Load pages |
| `browser_click` | Click elements |
| `browser_fill_form` | Complete forms |
| `browser_take_screenshot` | Capture visual state |
| `browser_console_messages` | Check for JS errors |
| `browser_resize` | Test responsive design |

---

## Project Structure

```
.claude/
├── agents/                 # Subagent definitions
│   ├── backend-engineer.md    # Backend/API specialist
│   ├── ui-engineer.md         # Frontend/Vue specialist
│   └── qa-expert.md           # Testing/QA specialist
├── rules/                  # Workflow rules
│   ├── structured-workflow.md # 4-phase development cycle
│   └── subagents-delegation.md # When to use which agent
└── skills/                 # Domain-specific knowledge
    ├── wayfinder-development/
    ├── pest-testing/
    └── developing-with-fortify/

app/
├── Http/
│   ├── Controllers/       # Inertia controllers
│   └── Requests/          # Form request validation
├── Models/                # Eloquent models
└── ...

resources/
└── js/
    ├── components/        # Reusable Vue components
    │   └── ui/            # shadcn-vue components
    ├── composables/       # Vue composables
    ├── layouts/           # Page layouts
    ├── pages/             # Inertia page components
    └── types/             # TypeScript definitions

tests/
├── Feature/               # Feature tests
└── Unit/                  # Unit tests
```

---

## The Agent System

This starter kit uses a **multi-agent orchestration pattern**. You (or the main Claude instance) act as the orchestrator, delegating work to specialized agents.

### How It Works

```
You (Orchestrator)
    │
    ├── Analyze request
    ├── Break into subtasks
    ├── Delegate to agents
    │
    ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│ backend-engineer│  │   ui-engineer   │  │    qa-expert    │
│                 │  │                 │  │                 │
│ • APIs          │  │ • Vue components│  │ • Test strategy │
│ • Database      │  │ • Inertia pages │  │ • E2E tests     │
│ • Auth/Authz    │  │ • shadcn-vue    │  │ • Bug hunting   │
│ • Queues        │  │ • TypeScript    │  │ • Performance   │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

### The 4-Phase Workflow

Every non-trivial task follows this cycle:

1. **Explore** — Gather context, read files, understand existing patterns
2. **Plan** — Design the implementation approach, present for approval
3. **Validate** — Wait for explicit user approval before writing code
4. **Implement** — Delegate to appropriate agents, execute the plan

This prevents wasted effort and ensures alignment with your vision.

### Example Delegation

```
User: "Add a contact form to the site"

Orchestrator thinking:
  → This needs a Vue page component (ui-engineer)
  → Needs an Inertia controller (backend-engineer)
  → Might need email sending logic (backend-engineer)
  → Should have tests (qa-expert)

Orchestrator: "I'll coordinate this across agents:
  1. backend-engineer for controller and email service
  2. ui-engineer for the Vue form component
  3. qa-expert for test coverage"
```

---

## Available Scripts

### Composer Scripts

```bash
# Start development (server + queue + logs + vite)
composer run dev

# Run all tests with linting
composer run test

# Format code with Pint
composer run lint

# Initial setup (install, migrate, build)
composer run setup
```

### NPM Scripts

```bash
# Build assets for production
npm run build

# Start Vite dev server with HMR
npm run dev

# Type check Vue components
npm run type-check

# Format frontend code
npm run format
```

### Artisan Commands

```bash
# Run tests
php artisan test --compact

# Run specific test
php artisan test --filter=ProfileUpdateTest

# Generate Wayfinder routes
php artisan wayfinder:generate

# List all routes
php artisan route:list
```

---

## Skills Reference

Skills activate automatically based on what you're working on:

| Skill | Activates When |
|-------|---------------|
| `wayfinder-development` | Importing routes from `@/actions` or `@/routes`, using type-safe route functions |
| `pest-testing` | Writing tests, TDD, assertions, debugging test failures, testing Inertia responses |
| `developing-with-fortify` | Authentication features, 2FA, password reset, email verification |

You can also manually invoke skills:

```
/wayfinder-development
/pest-testing
```

---

## Tips for Best Results

1. **Be specific about what you want** — "Add a contact form with name, email, and message fields that sends an email" is better than "add a form"

2. **Let the workflow guide you** — Don't skip the exploration and planning phases; they prevent rework

3. **Trust the agents** — Each agent is specialized; let them do their job

4. **Review the plans** — The validation phase exists for a reason; use it to catch misunderstandings early

5. **Use the MCP tools** — Laravel Boost's `search-docs` tool provides version-specific documentation that's invaluable

---

## Troubleshooting

### Vite manifest error

```
Illuminate\Foundation\ViteException: Unable to locate file in Vite manifest
```

Run `npm run build` or start the dev server with `npm run dev`.

### MCP server not connecting

1. Ensure the MCP server is installed (`npm list -g @anthropic-ai/mcp-playwright`)
2. Check your `settings.json` configuration
3. Restart Claude Code

### Tests failing after changes

```bash
# Clear config cache
php artisan config:clear

# Run tests
php artisan test --compact
```

### TypeScript errors

```bash
# Run type checking
npm run type-check

# Regenerate Wayfinder routes
php artisan wayfinder:generate
```

---

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

This project is open-sourced software licensed under the [MIT license](LICENSE).

---

Built with Laravel, Vue.js, Inertia.js, and Claude Code.
