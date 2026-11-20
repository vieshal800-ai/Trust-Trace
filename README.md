# BlueVault Security Gateway

A zero-trust entry gateway prototype for a hackathon — persona-based access control with distinct employee vs. attacker flows.

## Overview

This is the **entry gateway** (`index.html`) for a security demonstration. It presents two distinct personas:

| Persona | Origin IP | Network | Destination |
|---------|-----------|---------|-------------|
| **Employee (User)** | `192.168.1.105` | Branch Office /24 | `user.html` → `edit.html` |
| **External (Hacker)** | `203.0.113.88` | Public Internet /32 | `hacker.html` → `403.html` |

The gateway enforces IP-based routing at the UI layer — employees proceed to a detail-edit page, attackers are trapped at a 403 forbidden page.

## Features

- **Zero-trust visual language** — cyan for authorized, red for hostile
- **Animated background** — subtle grid + scanline overlay (60s loop)
- **3D card tilt** — perspective transform on mouse-move
- **Staggered entrance animations** — respects `prefers-reduced-motion`
- **Keyboard accessible** — focus states, Enter/Space activation
- **No build step** — pure HTML + Tailwind CDN + Font Awesome CDN

## Quick Start

```bash
# Serve locally (Python 3)
cd bluevault-gateway
python -m http.server 3003

# Open in browser
# http://localhost:3003
```

Or simply double-click `index.html` — no server required for static viewing.

## Project Structure

```
bluevault-gateway/
├── index.html          # Entry gateway (this file)
├── user.html           # Employee landing page (to be created)
├── edit.html           # User detail edit page (to be created)
├── hacker.html         # Attacker landing page (to be created)
├── 403.html            # Forbidden error page (to be created)
└── README.md           # This file
```

## Linked Pages (Not Yet Implemented)

The gateway references four destination pages that need to be created:

| File | Purpose |
|------|---------|
| `user.html` | Employee dashboard — shows authenticated user context |
| `edit.html` | User detail edit form — profile/credential management |
| `hacker.html` | Attacker trap page — collects Gmail/name/password (honeypot) |
| `403.html` | Forbidden page — shown after attacker submission |

## Tech Stack

- **HTML5** — semantic, accessible markup
- **Tailwind CSS** (CDN) — utility-first styling
- **Font Awesome 6** (CDN) — icons
- **Google Fonts** — Space Grotesk (display) + JetBrains Mono (data)
- **Vanilla JS** — parallax tilt, keyboard nav, intersection observer

## Customization

### Colors (CSS Custom Properties)

```css
:root {
  --cyan: #06b6d4;        /* Authorized actions */
  --red: #ef4444;         /* Hostile actions */
  --emerald: #10b981;     /* Success/allowed */
  --amber: #f59e0b;       /* Warning/network info */
  --bg-deep: #020617;     /* Page background */
  --bg-card: #0c1222;     /* Card surface */
  --bg-elevated: #111827; /* Elevated surface */
}
```

### Animation Timing

- Grid background: 60s linear loop
- Glow pulse: 4s ease-in-out
- Entrance stagger: 100ms increments
- Card hover: 400ms cubic-bezier(0.4, 0, 0.2, 1)

## Accessibility

- Semantic HTML5 (`header`, `main`, `button`, `a`)
- Focus-visible outlines (cyan/red per persona)
- Keyboard activation (Enter/Space on cards)
- `prefers-reduced-motion` respected — all animations disabled
- ARIA-compliant color contrast (WCAG AA)

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 15+
- Edge 90+

## License

Hackathon prototype — internal use only.