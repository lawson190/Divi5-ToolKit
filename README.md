# Divi5 Toolkit

The first Claude Code plugin for Divi 5 development. Validates CSS compatibility, generates Divi-ready code, scaffolds page sections, audits project health, checks accessibility, audits Core Web Vitals performance, diagnoses symptoms, learns from errors, and stays current with Divi 5 updates — all powered by Claude instead of GPT-3.5.

**For Divi 5.13+** (11 new modules since 5.6 — Timeline, Breadcrumbs, SVG, Table of Contents, Instagram Feed, Tooltip, Post Filter, Charts, Gravity Forms, Imagely Gallery, Payment Button — plus Gradient Variables, Variable Fonts, CSS Grid Editor, Loop Filters, Aspect Ratio/Framing, Variable Generators, pseudo-class editing, Composable Settings, Canvas system, Loop Builder)

## Why This Exists

Divi's built-in AI Agents (5.12+) only work inside the Visual Builder and only on what the builder exposes. This plugin gives you Claude with deep Divi 5 knowledge where the rest of your work happens — your CSS files, child theme, terminal, editor, and CI/CD pipeline. It knows Divi's selectors, specificity rules, breakpoints, Design Variables, Free-Form CSS, Composable Settings, Canvas system, and the full module library so you don't have to provide that context manually.

## Features

- **One-Command Setup**: `/divi5-toolkit:setup` detects your installed Divi version, child theme, and CSS prefix and writes the project config for you
- **Selector Lookup**: `/divi5-toolkit:selector blurb title` returns the wrapper, inner selectors, a paste-ready override, and the Free-Form CSS equivalent in seconds
- **CSS Generation**: Divi 5-ready CSS in four formats (Theme Options, Code Module, Child Theme, Free-Form CSS)
- **Section Scaffolding**: Complete page section templates (hero, pricing, FAQ, etc.) with CSS, responsive design, and accessibility baked in
- **Compatibility Validation**: Checks button specificity, numbered selectors, `!important` usage, CSS variable scope, format correctness, accessibility
- **Project Audit**: Whole-project CSS health scoring with graded report and prioritized fix list
- **Responsive Device Check**: Verifies a page at 9 real device sizes (360px Android through 2560px ultrawide) — live viewport testing + screenshots via a browser MCP server, or static CSS risk analysis without one
- **Accessibility Checking**: WCAG 2.1 AA compliance — focus indicators, color contrast, reduced motion, touch targets
- **Divi 5 Knowledge Base**: Complete selector reference, 20+ D5-native modules, Design Variable system, Preset hierarchy, responsive breakpoints, Composable Settings, Canvas system, Loop Builder + Loop Filters
- **Error Learning**: Paste Divi errors — the plugin analyzes, fixes, and remembers the pattern
- **Self-Updating**: `/divi5-toolkit:research` refreshes the plugin's own knowledge base from upstream Divi sources on demand (recommended weekly — check `last_research` in your config)
- **Migration Support**: Converts Divi 4 CSS patterns for Divi 5 compatibility
- **CSS Examples**: Animation patterns, dark mode, WooCommerce, accessibility fixes, design tokens, button variants

## Quickstart

Already have the plugin loaded? (See [Installation](#installation) if not.)

From your project root, in Claude Code:

```
/divi5-toolkit:setup
```

It reads `wp-content/themes/Divi/style.css` for the installed version, finds your child theme and existing CSS class prefix, asks at most three questions, and writes `.claude/divi5-toolkit.local.md`. (Manual alternative: copy `plugins/divi5-toolkit/templates/divi5-toolkit.local.md` to that path and edit `css_prefix`.)

Type `/divi5-toolkit:` — autocomplete should show all 10 commands. Try one:

```
/divi5-toolkit:generate primary button with gold hover state
```

You should get back Divi 5-ready CSS with `body` prefix, `!important`, your custom prefix, and paste instructions. That's it — you're up and running.

**Next steps:**
- [`docs/workflows.md`](docs/workflows.md) — Build a full landing page, migrate from Divi 4, audit a project, add dark mode, etc.
- [`docs/usage.md`](docs/usage.md) — What every command, agent, and skill does in detail
- [`docs/configuration.md`](docs/configuration.md) — Tune the plugin for your project type

## Commands

| Command | Description |
|---------|-------------|
| `/divi5-toolkit:setup` | Create or refresh the project config — auto-detects Divi version, child theme, CSS prefix |
| `/divi5-toolkit:selector` | Look up the right selector for any module/sub-element, with override + Free-Form patterns |
| `/divi5-toolkit:generate` | Generate Divi 5-ready CSS for any component |
| `/divi5-toolkit:validate` | Validate CSS for Divi 5 compatibility |
| `/divi5-toolkit:convert` | Convert existing CSS to Divi 5 format |
| `/divi5-toolkit:diagnose` | Diagnose a Divi 5 symptom/error and return root cause + fix |
| `/divi5-toolkit:research` | Research latest Divi 5 updates |
| `/divi5-toolkit:scaffold` | Generate complete page section templates |
| `/divi5-toolkit:audit` | Run a full project CSS audit with scoring |
| `/divi5-toolkit:responsive` | Check a page across device sizes (phones, tablets, laptops, widescreen) — live browser testing via MCP, or static CSS analysis |

## Agents

| Agent | Triggers When |
|-------|---------------|
| `divi5-validator` | After writing/editing CSS files (via PostToolUse hook, if `auto_validate: true`) |
| `divi5-error-learner` | When you paste Divi error messages or describe CSS issues |
| `divi5-researcher` | On-demand via `/divi5-toolkit:research` or when unknown Divi errors need research |
| `divi5-accessibility` | When reviewing CSS for accessibility, or when writing interactive element styles |
| `divi5-performance` | When the user mentions performance, Core Web Vitals (LCP, INP, CLS), slow Divi pages, render-blocking CSS, font loading, or cache-plugin conflicts |

## Skills

| Skill | Activates When |
|-------|----------------|
| `divi5-css-patterns` | Writing CSS for Divi, styling Divi modules |
| `divi5-compatibility` | Validating CSS, troubleshooting Divi issues |
| `divi5-performance` | Optimizing Divi performance, working with Critical CSS / Dynamic CSS / Inline Stylesheets, debugging LCP/INP/CLS, configuring local fonts and image preloading |

## Documentation

The tables above are quick references. For depth, see the `docs/` directory:

| Doc | What's Inside |
|---|---|
| [**`docs/usage.md`**](docs/usage.md) | Detailed reference: every command (purpose, args, example, output), every agent (triggers, behavior, output), every skill (when it activates, what it provides), every CSS example, every hook |
| [**`docs/configuration.md`**](docs/configuration.md) | Every config setting explained, with rationale and recommended values for solo dev, agency, government, WooCommerce, prototype, and legacy project types |
| [**`docs/workflows.md`**](docs/workflows.md) | Step-by-step guides: first-time setup, build a landing page, migrate from Divi 4, audit an inherited project, add dark mode, build a WooCommerce grid, off-canvas menu, accessibility compliance, debug "styles not applying", refresh knowledge base, check a page across device sizes |
| [**`docs/troubleshooting.md`**](docs/troubleshooting.md) | FAQ + diagnostic steps for plugin issues, Divi CSS issues, builder issues, plugin conflicts, migration issues, performance, and accessibility |

Internal docs:
- [`CLAUDE.md`](CLAUDE.md) — Developer guidance for working ON the plugin (architecture, conventions, contributing)
- [`STATE.md`](STATE.md) — Project state snapshot (current version, component inventory, knowledge topics)

## What the Plugin Knows

### Divi 5 Architecture
- React 18-based, no Shadow DOM — standard DOM with `et_pb_*` classes
- JSON block storage (no shortcodes)
- Dynamic CSS (94% smaller stylesheets)
- Critical CSS (eliminates render-blocking requests)
- Composable Settings (5.2) — toggle any design option on any sub-element

### CSS Integration Methods
1. Theme Options (global, no tags)
2. Page-Level CSS
3. **Free-Form CSS** with `selector` keyword (new in D5)
4. Module Element fields (properties only)
5. Code Module (with `<style>` tags)
6. **Custom HTML Wrappers** (new in D5)
7. **Semantic Elements** (new in D5)
8. Child Theme
9. **Attributes Panel** (replaces old CSS ID & Classes)

### Module Library
- 40+ built-in modules with complete selector reference
- 20+ D5-native modules: Group, Carousel Group, Before/After Image, Canvas Portal, Dropdown, Icon List, Link, Lottie, Timeline, Breadcrumbs, SVG, Table of Contents, Instagram Feed (5.6), Tooltip (5.8), Post Filter + Post Filter Item (5.10), Charts, Gravity Forms, Imagely Gallery, Payment Button (5.11)
- Contact Form 7 Styler (5.3)
- 17+ WooCommerce product modules

### Canvas System (New in D5)
- **Main Canvas** — primary page content
- **Local Canvases** — per-page detached workspaces
- **Global Canvases** — site-wide reusable canvases
- **Canvas Portal Module** — inject canvas content at specific locations
- **Interaction Builder** — cross-canvas interactions (Click, Mouse, Viewport, Load triggers)
- Off-canvas menus, popups, mega menus, staging areas

### Design System
- 7 Design Variable types (Colors, Fonts, Numbers, Images, Text, Links, Gradients)
- Variable Generators: Sizing (5.4), Relative Colorscheme (5.4), Color Scale + Harmony (5.6)
- 4-tier Preset hierarchy (Option Group, Element, Stacked, Nested)
- Composable Settings — enable any option on any sub-element
- Variable Fonts + advanced typography controls (5.9), visual CSS Grid Editor (5.9)
- CSS custom properties fully supported

### Responsive Design
- 7 breakpoints (3 active by default: Phone 767px, Tablet 980px, Desktop)
- 4 optional: Phone Wide 860px, Tablet Wide 1024px, Widescreen 1280px, Ultra Wide 2560px
- All breakpoint widths customizable

### Accessibility Support
- Semantic Elements (change div to nav, header, section, etc.)
- ARIA attributes via Attributes panel
- Focus indicator patterns (Divi removes defaults)
- Reduced motion support
- WCAG 2.1 AA color contrast guidance
- Touch target sizing

### Troubleshooting Knowledge
- Cache plugin conflicts (WP Rocket RUCSS, LiteSpeed, Autoptimize)
- Security plugin issues (Wordfence firewall)
- WooCommerce styling problems
- Divi 4 to 5 migration patterns
- Debugging with Safe Mode, DevTools, D5 Dev Tool
- Divi 5.2–5.13 bug fix history (transform corruption, box-shadow hover, loop CSS, linter false positives, cache-related style loss, preset-class override, migrated Free-Form CSS, and the per-version fixes documented in the compatibility skill)

### CSS Example Library
- **Button Variants** — primary, secondary, outline, sizes
- **Design Tokens** — complete design system template
- **Animations** — fade, slide, scale, stagger, hover effects with reduced-motion
- **Dark Mode** — system-aware with manual toggle
- **WooCommerce** — product grids, cards, cart, checkout
- **Accessibility** — focus indicators, skip links, screen reader utilities, high contrast
- **Responsive 7-Breakpoints** — full 2025-aligned breakpoint template
- **Loop Builder** — CSS Grid card layouts, masonry, product cards, horizontal lists, pagination
- **Forms** — Divi 5.3 pseudo-class editing (:checked/:focus/:active), custom checkboxes/radios, Contact Form 7 Styler
- **New Modules (5.6–5.11)** — Timeline, Breadcrumbs, SVG, Table of Contents, Instagram Feed, Tooltip, Post Filter, Gravity Forms, Charts, Payment Button styling
- **Critical CSS** — hand-crafted above-the-fold template (in divi5-performance skill)
- **Font Loading** — local @font-face with CLS-prevention metric overrides (in divi5-performance skill)

## Optional MCP Servers

No MCP servers required. For extended capabilities, add to your `.mcp.json`:

### Context7 (Documentation Lookup)
```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

### Playwright (Browser Testing)
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

### A11y (Accessibility Testing)
```json
{
  "mcpServers": {
    "a11y": {
      "command": "npx",
      "args": ["-y", "a11y-mcp"]
    }
  }
}
```

**Windows users:** Wrap in `"command": "cmd", "args": ["/c", "npx", "-y", "..."]`

## Configuration

Create `.claude/divi5-toolkit.local.md` in your project root. Full template at `plugins/divi5-toolkit/templates/divi5-toolkit.local.md`.

Key settings:

```yaml
validation_mode: advisory             # "advisory" (warnings) or "strict" (blocking errors)
default_format: theme-options         # "theme-options" | "code-module" | "child-theme" | "free-form"
auto_validate: true                   # validate CSS files automatically after Write/Edit
divi_version: "5.13"                  # target Divi version — set by /setup, read by most commands
css_prefix: my                        # your custom CSS class prefix
active_breakpoints:                   # which of Divi 5's 7 breakpoints to use
  - phone
  - tablet
  - desktop
accessibility_level: aa               # "aa" | "aaa" | "off" — strictness of accessibility checks
flag_composable_alternatives: true    # suggest builder-native alternatives to custom CSS (Divi 5.2+)
scaffold_style: light                 # "light" | "dark" | "brand" — default color scheme for /scaffold
last_research: 2026-09-25             # auto-updated by divi5-researcher
```

**What each setting affects:**

| Setting | Read by |
|---------|---------|
| `validation_mode` | `/validate`, `divi5-validator` |
| `default_format` | `/generate`, `/scaffold`, `/convert` |
| `auto_validate` | PostToolUse hook |
| `divi_version` | `/setup` (writes), `/selector`, `/generate`, `/audit`, `/diagnose`, `/responsive`, `divi5-performance` |
| `css_prefix` | `/setup` (writes), `/selector`, `/generate`, `/scaffold`, `/convert`, `/diagnose`, `/responsive` |
| `active_breakpoints` | `/generate`, `/scaffold`, `/responsive` |
| `accessibility_level` | `/validate`, `/audit`, `/diagnose`, `/responsive`, `divi5-accessibility` |
| `flag_composable_alternatives` | `/validate`, `/convert`, `/audit` |
| `scaffold_style` | `/scaffold` |
| `last_research` | `/research`, `divi5-researcher` |

## Installation

There are two ways to load the plugin: per-session (one-off) or persistent (auto-loads in specific projects or globally).

### Option 1 — Per-session (one-off, no setup)

From your project directory, start Claude Code with the `--plugin-dir` flag:

```bash
claude --plugin-dir "/path/to/Divi5-ToolKit/plugins/divi5-toolkit"
```

The plugin loads for that session only. Use this for testing or occasional use.

### Option 2 — Per-project (recommended for active Divi work)

Auto-load the plugin whenever you start Claude Code in a specific project. This uses Claude Code's local marketplace mechanism — no actual marketplace publication required.

In your website project root, create `.claude/settings.local.json` (gitignored — keeps your absolute path machine-local):

```json
{
  "extraKnownMarketplaces": {
    "divi5-local": {
      "source": {
        "source": "directory",
        "path": "/absolute/path/to/Divi5-ToolKit"
      }
    }
  },
  "enabledPlugins": {
    "divi5-toolkit@divi5-local": true
  }
}
```

Make sure `.claude/settings.local.json` is in your project's `.gitignore` so the absolute path doesn't get committed:

```
.claude/settings.local.json
.claude/*.local.json
```

Then start Claude Code from the project directory — `/divi5-toolkit:` should autocomplete.

### Option 3 — Global (always loaded everywhere)

Same JSON as Option 2, but write it to `~/.claude/settings.json` instead of the per-project file. The plugin will be available in every Claude Code session on your machine.

### How it works

The Divi5-ToolKit ships with `.claude-plugin/marketplace.json` (the marketplace manifest) alongside `.claude-plugin/plugin.json` (the plugin manifest). Claude Code looks for `marketplace.json` at exactly that path inside any directory you register via `extraKnownMarketplaces`.

The `extraKnownMarketplaces` entry in your settings tells Claude Code to treat the local directory as a marketplace; Claude reads `.claude-plugin/marketplace.json` from that directory to discover what plugins are available; `enabledPlugins` activates the plugin from that marketplace.

The marketplace name is `divi5-local` (declared inside `.claude-plugin/marketplace.json`). It must match the key you use in `extraKnownMarketplaces` and the part after the `@` in `enabledPlugins`. The reference patterns in the JSON above use that name verbatim — change them in lockstep if you want a different name.

No publication, validation, or CLI registration step is needed.

## Directory Structure

```
divi5-toolkit/                            # ← repo root + marketplace root
├── .claude-plugin/
│   └── marketplace.json                 # Marketplace manifest (lists plugins)
├── plugins/
│   └── divi5-toolkit/                   # ← plugin lives in a subdirectory
│       ├── .claude-plugin/
│       │   └── plugin.json              # Plugin manifest (name, version)
│       ├── commands/                     # Slash commands
│       │   ├── setup.md                 # NEW v2.5.0
│       │   ├── selector.md              # NEW v2.5.0
│       │   ├── generate.md
│       │   ├── validate.md
│       │   ├── convert.md
│       │   ├── diagnose.md              # NEW v2.2.0
│       │   ├── research.md
│       │   ├── scaffold.md
│       │   ├── audit.md
│       │   └── responsive.md             # NEW v2.3.0
│       ├── agents/                       # Autonomous agents
│       │   ├── divi5-validator.md
│       │   ├── divi5-error-learner.md
│       │   ├── divi5-researcher.md
│       │   ├── divi5-accessibility.md
│       │   └── divi5-performance.md     # NEW v2.2.0
│       ├── skills/                       # Auto-activating skills
│       │   ├── divi5-css-patterns/
│       │   │   ├── SKILL.md
│       │   │   ├── examples/
│       │   │   │   ├── button-variants.css
│       │   │   │   ├── design-tokens.css
│       │   │   │   ├── animations.css
│       │   │   │   ├── dark-mode.css
│       │   │   │   ├── woocommerce.css
│       │   │   │   ├── accessibility.css
│       │   │   │   ├── responsive-7-breakpoints.css
│       │   │   │   ├── loop-builder.css          # NEW v2.2.0
│       │   │   │   ├── forms.css                 # NEW v2.2.0
│       │   │   │   └── new-modules.css           # NEW v2.2.0
│       │   │   └── references/
│       │   │       ├── divi-selectors.md
│       │   │       └── responsive-breakpoints-2025.md
│       │   ├── divi5-compatibility/
│       │   │   ├── SKILL.md
│       │   │   └── references/
│       │   │       └── unit-conversions.md
│       │   └── divi5-performance/                # NEW v2.2.0
│       │       ├── SKILL.md
│       │       ├── examples/
│       │       │   ├── critical-css.css
│       │       │   └── font-loading.css
│       │       └── references/
│       │           └── core-web-vitals.md
│       ├── hooks/
│       │   ├── hooks.json               # Event handlers
│       │   └── css-validate.sh
│       ├── templates/
│       │   └── divi5-toolkit.local.md   # Configuration template
│       └── .mcp.json
├── docs/                                 # End-user documentation
│   ├── usage.md                         # Detailed component reference
│   ├── configuration.md                 # Config setting reference
│   ├── workflows.md                     # Step-by-step scenarios
│   └── troubleshooting.md               # FAQ + diagnostic steps
├── scripts/
│   └── lint.sh                          # Repo lint (frontmatter, JSON, docs coverage) — NEW v2.5.0
├── .github/workflows/validate.yml        # CI: lint + `claude plugin validate .` — NEW v2.5.0
├── CLAUDE.md                             # Developer guidance (working ON the plugin)
├── STATE.md                              # Project state snapshot
└── README.md
```

## Changelog

### Unreleased

- **Knowledge:** new "Page conten