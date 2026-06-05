# Nuxt SaaS Template

[![Nuxt UI](https://img.shields.io/badge/Made%20with-Nuxt%20UI-00DC82?logo=nuxt&labelColor=020420)](https://ui.nuxt.com)

Fully built SaaS application to launch your next project with a landing page, a pricing page, a documentation and a blog powered by [Nuxt UI](https://ui.nuxt.com) components.

- [Live demo](https://saas-template.nuxt.dev/)
- [Documentation](https://ui.nuxt.com/docs/getting-started/installation/nuxt)

<a href="https://saas-template.nuxt.dev/" target="_blank">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://ui.nuxt.com/assets/templates/nuxt/saas-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://ui.nuxt.com/assets/templates/nuxt/saas-light.png">
    <img alt="Nuxt SaaS Template" src="https://ui.nuxt.com/assets/templates/nuxt/saas-light.png">
  </picture>
</a>

## Quick Start

```bash [Terminal]
npm create nuxt@latest -- -t ui/saas
```

## Deploy your own

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-name=saas&repository-url=https%3A%2F%2Fgithub.com%2Fnuxt-ui-templates%2Fsaas&demo-image=https%3A%2F%2Fui.nuxt.com%2Fassets%2Ftemplates%2Fnuxt%2Fsaas-dark.png&demo-url=https%3A%2F%2Fsaas-template.nuxt.dev%2F&demo-title=Nuxt%20SaaS%20Template&demo-description=A%20SaaS%20template%20with%20landing%2C%20pricing%2C%20docs%20and%20blog%20powered%20by%20Nuxt%20Content.)

## Setup

Make sure to install the dependencies:

```bash
pnpm install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
pnpm dev
```

## Production

Build the application for production:

```bash
pnpm build
```

Locally preview production build:

```bash
pnpm preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.

## Renovate integration

Install [Renovate GitHub app](https://github.com/apps/renovate/installations/select_target) on your repository and you are good to go.

---

## USWDS Design System Customization

This project was restyled to follow the [U.S. Web Design System (USWDS)](https://designsystem.digital.gov/) — the official design language used by U.S. federal government websites. Below is a detailed record of every change made, why it was made, and how to replicate or extend it.

---

### 1. Typography — `app/assets/css/main.css`

#### What changed
A USWDS-aligned type scale was added inside the `@theme static` block in Tailwind CSS v4.

```css
@theme static {
  --font-sans: 'Public Sans', sans-serif;

  /* USWDS Type Scale */
  --text-2xs: 0.625rem;  /* 10px */
  --text-xs:  0.75rem;   /* 12px */
  --text-sm:  0.875rem;  /* 14px */
  --text-md:  1rem;      /* 16px — replaces Tailwind's `text-base` */
  --text-lg:  1.125rem;  /* 18px */
  --text-xl:  1.25rem;   /* 20px */
  --text-2xl: 1.5rem;    /* 24px */
  --text-3xl: 1.75rem;   /* 28px */
  --text-4xl: 2rem;      /* 32px */
  --text-5xl: 2.5rem;    /* 40px */
  --text-6xl: 3rem;      /* 48px */

  /* USWDS Semantic Heading Sizes */
  --text-h1: 2.44rem;
  --text-h2: 1.95rem;
  --text-h3: 1.34rem;
  --text-h4: 1.07rem;
  --text-h5: 0.93rem;
  --text-h6: 0.87rem;
}
```

#### Why
USWDS uses token names like `2xs`, `xs`, `sm`, `md` — **not** Tailwind's `base`. The token `--text-md` is the USWDS default body size (16px). Using `md` keeps naming consistent with USWDS documentation.

#### Usage in templates
```vue
<h1 class="text-4xl">Heading</h1>
<p class="text-md">Body paragraph</p>
<small class="text-xs">Caption</small>
```

> **Note:** Any existing use of `text-base` in templates must be updated to `text-md`.

---

### 2. Auth Layout — `app/layouts/auth.vue`

The auth layout wraps the `/login` and `/signup` pages. It was fully replaced with a USWDS government page shell.

#### Structure
```
┌─────────────────────────────────────────────┐
│  Gov banner ("An official website of…")      │  bg #f0f0f0, text-xs
├─────────────────────────────────────────────┤
│  Site header                                 │  bg #162e51 (navy), text white
│  [Logo]                [Agency Contact]      │
├─────────────────────────────────────────────┤
│  Page background: #f0f0f0                    │
│  ┌───────────────────────────────────────┐  │
│  │  White card, border-l-4 #005ea2       │  │  ← This is the texture/lift
│  │  <slot />                             │  │
│  └───────────────────────────────────────┘  │
├─────────────────────────────────────────────┤
│  Footer                                      │  bg #162e51 (same navy)
└─────────────────────────────────────────────┘
```

#### Key decisions

- **Page background `#f0f0f0`** — USWDS uses a light gray page background so the white content card reads as a lifted surface. Without this, the page looks flat (white on white).
- **`border-l-4 border-[#005ea2]`** — The blue left border is a classic USWDS affordance that anchors the content card and signals an interactive or important section.
- **`shadow-sm`** — A subtle shadow adds just enough depth to separate the card from the gray background without feeling like a commercial product.
- **The gov banner** uses a simplified US flag SVG. USWDS mandates this banner on all official pages.

---

### 3. Login & Signup Pages — `app/pages/login.vue`, `app/pages/signup.vue`

#### Layout: Two-column grid

```vue
<div class="grid grid-cols-1 lg:grid-cols-2 gap-10 lg:gap-16 items-start">
  <!-- Left: form -->
  <!-- Right: benefits panel -->
</div>
```

- **`grid-cols-1`** on mobile, **`lg:grid-cols-2`** on desktop — standard responsive pattern.
- **`gap-10 lg:gap-16`** — tighter gap on tablet, wider on desktop for breathing room.
- **`items-start`** — aligns both columns to the top, so the form doesn't stretch to match the benefits panel height.

#### Buttons

All buttons are **filled** — no ghost/outline buttons. USWDS guidelines treat outline buttons as rarely-used secondary affordances. The two button tiers used here:

| Button | Color | Use |
|---|---|---|
| Primary action | `bg-[#005ea2]` (USWDS blue) | Sign in, Create account |
| Secondary action | `bg-[#d9e8f6]` (light blue), dark text | Login.gov SSO |

```vue
<!-- Primary -->
<UButton class="bg-[#005ea2] hover:bg-[#1a4480] text-white" />

<!-- Secondary (filled, not outline) -->
<UButton class="bg-[#d9e8f6] hover:bg-[#aacdec] text-[#1a4480] font-semibold" />
```

#### Benefits list — icon optical alignment

This is the trickiest part. Icons adjacent to multi-line text must align to the **cap-height of the first line**, not the vertical center of the whole block.

```vue
<li class="flex gap-2 items-start">
  <UIcon
    name="i-lucide-check"
    class="text-[#005ea2] shrink-0 w-5 h-5 self-start translate-y-px"
  />
  <div>
    <p class="text-sm font-semibold">Benefit description.</p>
    <p class="text-sm text-neutral-500">Supporting detail text.</p>
  </div>
</li>
```

**Why each class:**
- `flex gap-2 items-start` — flex row, 8px gap, children align to the top of the container
- `w-5 h-5` — 20px icon, large enough to read as a real visual element (not decorative)
- `self-start` — prevents the icon from stretching with the flex container
- `translate-y-px` — a 1px downward nudge to optically align the icon stroke with the cap-height of the bold label text. This compensates for the internal padding most SVG icons carry at their top edge.
- `shrink-0` — prevents the icon from compressing when the container is narrow

> Without `translate-y-px`, the checkmark appears to float above the text baseline. Without `self-start`, it centers vertically in the two-line block, making it appear too low.

---

### 4. Error Page — `app/error.vue`

Replaced the default `<UError>` component with a custom USWDS 404 layout:

- Breadcrumb: `Home / Page not found`
- Error code display
- Two actions: **Go back** (primary) and **Continue to homepage** (secondary)
- Helpful links list with icons
- Same gov banner + navy header + navy footer as the auth layout

---

### 5. Color Reference

| Token | Hex | Use |
|---|---|---|
| USWDS Blue | `#005ea2` | Links, primary buttons, icon color, left border accent |
| USWDS Dark Blue | `#1a4480` | Button hover state |
| USWDS Light Blue | `#d9e8f6` | Secondary button fill |
| USWDS Navy | `#162e51` | Header, footer backgrounds |
| USWDS Gray | `#f0f0f0` | Page background, gov banner |
| USWDS Border | `#dfe1e2` | Subtle separators |
| Error Red | `#b50909` | Form validation errors |

---

### 6. How to Change Colors (Step-by-Step for Beginners)

Colors in this project live in **two places** depending on what you want to change.

---

#### A. Brand palette colors (used in Tailwind classes like `bg-brand-500`)

Open `app/assets/css/main.css`. You'll see two color scales defined as CSS variables inside `@theme static`:

```css
@theme static {
  /* Orange Brand — used as the primary UI color */
  --color-brand-50:  #fff4ee;   /* lightest tint */
  --color-brand-500: #f15a22;   /* main brand color */
  --color-brand-950: #400e07;   /* darkest shade */

  /* Navy — used as the secondary UI color */
  --color-navy-900: #1e2d4e;    /* used in header/footer */
}
```

To change the brand to a different color, replace the hex values. For example, to switch to a green brand:

```css
--color-brand-500: #2e8540;   /* USWDS green */
```

These variables are registered with Tailwind, so you can immediately use them as classes anywhere in your `.vue` files:

```vue
<div class="bg-brand-500 text-white">Hello</div>
<div class="text-brand-700">Muted brand text</div>
<div class="border-brand-300">Subtle border</div>
```

The number scale works like paint chips: `50` is nearly white, `500` is the true color, `950` is nearly black. You need all 11 steps (`50`, `100`, `200` ... `950`) for Tailwind to generate every shade variant.

> **Tip:** Use [USWDS Color Tool](https://designsystem.digital.gov/design-tokens/color/overview/) or [Tailwind Shades](https://www.tailwindshades.com/) to generate a full 11-step scale from any hex color.

---

#### B. USWDS structural colors (header, footer, buttons, links)

These are hardcoded as inline Tailwind arbitrary values in the layout and page files. They look like this:

```vue
<header class="bg-[#162e51]">...</header>
<UButton class="bg-[#005ea2] hover:bg-[#1a4480]" />
```

To change the header color, for example, find `bg-[#162e51]` in `app/layouts/auth.vue` and replace the hex:

```vue
<!-- Before -->
<header class="bg-[#162e51] text-white">

<!-- After: switch to a dark green header -->
<header class="bg-[#1a4f23] text-white">
```

The same pattern applies to the footer — it uses the same `#162e51` value, so search for it in both places.

---

#### C. Where each color is used at a glance

```
app/assets/css/main.css
  └── --color-brand-*    →  bg-brand-*, text-brand-*, border-brand-*
  └── --color-navy-*     →  bg-navy-*, text-navy-*, border-navy-*

app/layouts/auth.vue
  └── #162e51            →  header background, footer background
  └── #005ea2            →  left border accent on the white card
  └── #f0f0f0            →  page background (gray field)

app/pages/login.vue
app/pages/signup.vue
  └── #005ea2            →  primary button, checkmark icons, links
  └── #1a4480            →  button hover state
  └── #d9e8f6            →  secondary button (Login.gov) fill
  └── #aacdec            →  secondary button hover
  └── #f0f4f9            →  benefits panel background

app/error.vue
  └── #162e51            →  header, footer
  └── #005ea2            →  links, primary button, breadcrumb
```

---

#### D. Nuxt UI component colors (the `primary` and `secondary` system)

Nuxt UI has its own color system that maps `primary` and `secondary` to your brand palette. This is configured in two places:

**`nuxt.config.ts`:**
```ts
ui: {
  colors: {
    primary: 'brand',    // maps to --color-brand-* from main.css
    secondary: 'navy',   // maps to --color-navy-* from main.css
    neutral: 'neutral'
  }
}
```

**`app/app.config.ts`:**
```ts
export default defineAppConfig({
  ui: {
    colors: {
      primary: 'blue',    // Nuxt UI built-in palette fallback
      neutral: 'slate'
    }
  }
})
```

So if you write `<UButton color="primary" />`, Nuxt UI resolves `primary` → `brand` → `--color-brand-500`. Changing `primary: 'brand'` to `primary: 'emerald'` would switch all primary UI components to Tailwind's built-in emerald green scale instantly.
