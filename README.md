---
name: "MyFlicker Design System"
---

# MyFlicker Design System

MyFlicker Design System is a Light-mode design library for building consistent product surfaces for the MyFlicker product. Visual behavior resolves through Light tokens; legacy token names remain as compatibility aliases.

## 里程碑状态

| 里程碑 | 内容 | 状态 |
|--------|------|------|
| M1 Token 层 | 334 个 CSS 变量，52/52 Figma 语义 token 100% 覆盖 | ✅ 已完成 |
| M2 组件层 | 15 个组件 + 204 图标库接入（`@kid/enterprise-icon`） | ✅ 已完成 |
| M3 AI 合约层 | `SKILL.md` / `library-consumption.json` / `README.md` / `components/index.json` | ✅ 已完成 |
| M4 UI Kit 场景页 | 5 个典型页面场景（chat-main × 3 + list-page + setting） | ✅ 已完成 |

---

## Open the Showcases

All pages are static HTML and link the shared files in this directory.

| Showcase | Path | Status |
|---|---|---|
| Component previews | `preview/component-*.html` | ✅ M4 current |
| Icon browser | `preview/icon-browser.html` | ✅ M4 current |
| **UI Kit - Chat 欢迎态** | `ui_kits/chat-main/index.html` | ✅ M4 current |
| **UI Kit - Chat 对话态** | `ui_kits/chat-main/chatting.html` | ✅ M4 current |
| **UI Kit - Chat 资产预览面板** | `ui_kits/chat-main/chatting-asset-panel.html` | ✅ M4 current |
| **UI Kit - 列表页** | `ui_kits/list-page/index.html` | ✅ M4 current |
| **UI Kit - 设置页** | `ui_kits/setting/index.html` | ✅ M4 current |

> All pages use `.mf-*` classes, `colors_and_type.css` tokens, and `assets/icons/kid/` icons.

## AI-Native Iteration

Each M4 ui_kit directory contains a `_scene.md` manifest. **Always read `_scene.md` before editing any page file** — it maps all editable zones, components used, design constraints, and common intent patterns for that page.

```
ui_kits/{page}/
  _scene.md      ← read this first (zone map, constraints, intent examples)
  index.html     ← default / welcome state
  chatting.html  ← (where applicable) conversation state
```

**Workflow for natural-language design iteration:**
1. AI reads `_scene.md` → locates the target zone
2. AI edits the relevant `.html` file surgically (never rewrites the whole file)
3. Preview at `http://localhost:8080/ui_kits/{page}/index.html`

## Consumption Contract

| Layer | Files | Use |
|---|---|---|
| Tokens | `colors_and_type.css`, `css.json` | Light-mode design language and compatibility aliases |
| Components | `components.css`, `components/index.json`, `components/{slug}.json`, `preview/component-*.html` | Stable `.mf-*` atoms, component markup, classes, consumed tokens, DOM anatomy, assets, and provenance |
| Icons | `assets/icons/kid/*.svg`, `assets/icons/kid/icon-list.json` | MyFlicker icon library (204 icons, from `@kid/enterprise-icon`) |
| UI Kits | `ui_kits/{type}/index.html` (legacy) | Page-level showcase evidence only — do not copy as production templates |

Start with `library-consumption.json` when consuming this package from another project.

## Component Classes

All components use the `.mf-` prefix:

| Group | Key Classes |
|---|---|
| Action | `.mf-btn`, `.mf-btn--primary`, `.mf-btn--secondary`, `.mf-btn--tertiary`, `.mf-btn--ghost`, `.mf-btn--danger` |
| Form | `.mf-input`, `.mf-textarea`, `.mf-select`, `.mf-checkbox`, `.mf-radio`, `.mf-switch` |
| Display | `.mf-card`, `.mf-tag`, `.mf-avatar`, `.mf-table`, `.mf-progress`, `.mf-skeleton` |
| Navigation | `.mf-tabs`, `.mf-tabs--pill`, `.mf-breadcrumb`, `.mf-pagination`, `.mf-menu` |
| Overlay | `.mf-dialog`, `.mf-popover`, `.mf-tooltip` |
| Feedback | `.mf-alert`, `.mf-alert--info`, `.mf-alert--success`, `.mf-alert--warning`, `.mf-alert--error` |

## Icon System

**Primary source:** `assets/icons/kid/` — MyFlicker icons from `@kid/enterprise-icon`

- Browse icons: open `preview/icon-browser.html` (search + click to copy name)
- Icon index: `assets/icons/kid/icon-list.json` (204 icons as of v1.0.1023)
- All icons: `viewBox="0 0 1024 1024"`, `fill="currentColor"` — inherit parent `color`
- Sync latest: `zsh scripts/sync-icons.sh`

**Inline usage:**
```html
<span class="icon" style="width:16px;height:16px;" aria-hidden="true"
      data-asset-icon="assets/icons/kid/{name}.svg">
  <!-- paste SVG from assets/icons/kid/{name}.svg -->
</span>
```
```css
/* Required in component CSS block */
.icon svg, .icon svg * { fill: currentColor; }
```

## Machine-readable Data Shape

- `library-consumption.json` — routing contract; use to choose the correct layer for a task
- `css.json` — grouped token projection under `color`, `font`, `radius`, `spacing`, `size`, `shadow`
- `components/{slug}.json` — component contracts; key fields: `tokensConsumed`, `domAnatomy`, `assetsConsumed`, `coverageMatrix`, `provenance`
- `assets/icons/kid/icon-list.json` — icon name, viewBox, and file path for each MyFlicker icon

## Token Highlights

| Group | Examples |
|---|---|
| Surface | `--bg-base-default`, `--bg-base-secondary`, `--bg-overlay-l1..l4`, `--bg-menu` |
| Brand | `--bg-brand`, `--bg-brand-hover`, `--bg-brand-popup` |
| Text / Icon | `--text-default`, `--text-secondary`, `--text-tertiary`, `--icon-default`, `--icon-secondary`, `--icon-tertiary` |
| Border | `--border-neutral-l1..l3`, `--border-contrast`, `--border-brand` |
| Type | `--body-sm-*`, `--body-md-*`, `--heading-*`, `--code-editor-*`, `--font-family-metric` |
| Radii | `--radius-0`, `--radius-2..32`, `--radius-full` |
| Spacing | `--spacer-0`, `--spacer-2..64` |
| Status | `--status-success-*`, `--status-warning-*`, `--status-error-*`, `--status-info-*` |

## Known Limitations

- Component contracts are medium-confidence implementation contracts derived from preview pages. Validate against rendered previews before treating them as final design intent.
- M4 UI Kit 场景页全部完成：chat-main（欢迎态 / 对话态 / 资产预览面板）、list-page、setting 共 5 个页面。
- Dark mode is out of scope for this library version.

## Authoring Rules

1. Use tokens from `colors_and_type.css`; do not add raw colors or new ad hoc scales.
2. Use `.mf-*` component classes from `components.css` before adding page-local styles.
3. Use `assets/icons/kid/{name}.svg` for all icons in new work.
4. Keep Light mode as the shipped mode. Do not add dark overrides unless migration scope changes.
5. Keep existing file names and directories stable for downstream consumers.
6. Keep `components/{slug}.json`, `components/index.json`, and `library-consumption.json` synchronized when component APIs change.
7. To refresh icons: `zsh scripts/sync-icons.sh` from project root.
