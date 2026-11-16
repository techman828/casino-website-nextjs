# Casino M8trix Website

A responsive casino and hospitality marketing website built with Next.js. It presents Casino M8trix's gaming offerings, restaurants, events, card tutorials, community information, and job listings through a dark theme with red accents, photography, video, and animated components.

The repository is a frontend implementation. Content is defined in pages and components; there is no database, authentication system, payment flow, or playable wagering engine.

## Features

- Homepage with an autoplaying muted video, jackpot displays, dining highlights, and a rotating image carousel.
- Gaming overview, jackpot information, and a three-card poker detail page.
- Dining pages for Zone 8 Sports Bar, Epic Bar, Parallel Lounge, and Lotus Cafe.
- Event and promotion pages, including the event tower.
- Card Academy tutorials and gaming tips.
- About, community, contact, and employment pages, including job preview modals.
- Desktop dropdown navigation, mobile navigation, reusable layouts, and animated modals.
- A loading overlay that waits for fonts and selected images.

## Technology

| Area | Implementation |
| --- | --- |
| Framework | Next.js 16.0.0, App Router |
| UI | React 19.2 |
| Language | TypeScript with strict checking |
| Styling | Tailwind CSS 4 and global CSS |
| Animation | Framer Motion 12 |
| Icons | Font Awesome, Lucide React, React Icons, and custom SVG components |
| Tooling | ESLint 9 with Next.js presets; webpack for development and production builds |

## Getting started

Use Node.js **20.9 or newer** and npm. The repository includes `package-lock.json` for dependency installation.

From the repository root:

```sh
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000). Edit `app/page.tsx` to change the homepage.

On Windows PowerShell, if script execution policy blocks `npm.ps1`, use `npm.cmd` in place of `npm`, for example `npm.cmd ci` and `npm.cmd run dev`.

### Commands

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the development server with webpack |
| `npm run build` | Generate the production build with webpack |
| `npm start` | Serve a completed production build |
| `npm run lint` | Run ESLint across the project |
| `npx tsc --noEmit` | Check TypeScript without emitting files |

There is no automated test suite or `test` script configured.

The documentation review found that TypeScript checking passes, while ESLint reports 4 errors and 18 warnings. The errors are explicit `any` types in `app/components/gaming/trCom.tsx` and `app/components/icons/molicule.tsx`. The production build was stopped after remaining at the compile stage for over two minutes without further output; a successful production build has not been verified.

## Routes

These paths reflect the existing `app/` directories. Preserve their spelling and capitalization when linking, especially on case-sensitive deployment systems.

| Section | Routes |
| --- | --- |
| Home | `/` |
| Gaming | `/gaming`, `/gaming/jackpot`, `/gaming/threeCardGame` |
| Dining | `/dining`, `/dining/sportsBar`, `/dining/EpicBar`, `/dining/parallel`, `/dining/cafe` |
| Events | `/events`, `/events/blackJack`, `/events/drink`, `/events/gaming`, `/events/liquid`, `/events/oysters`, `/events/tower` |
| Card Academy | `/cardacadamy`, `/cardacadamy/baccaratGold`, `/cardacadamy/gamigTip`, `/cardacadamy/pure`, `/cardacadamy/threecard` |
| Information | `/about`, `/community`, `/contact`, `/employment` |
| Error display | `/error`; unmatched URLs use `app/not-found.tsx` |

`cardacadamy` and `gamigTip` are the current directory names, including their typos. Renaming them also requires updating links throughout the app.

## Project structure

```text
app/
  page.tsx               Homepage
  layout.tsx             Root metadata, Google fonts, analytics, loading wrapper
  loading.tsx            Asset-loading overlay
  not-found.tsx          Custom 404 page
  globals.css            Tailwind import, theme, fonts, shared styles
  fontawesome.ts         Font Awesome setup
  about/                 About page
  cardacadamy/           Tutorials and gaming tips
  community/             Community information
  contact/               Contact information and message UI
  dining/                Restaurants and bars
  employment/            Job listings
  events/                Events and promotions
  gaming/                Game and jackpot information
  error/                 Standalone error display page
  components/            Shared and section-specific UI
public/
  assets/fonts/          Local Nunito and Big Noodle Titling fonts
  assets/images/         Photos, backgrounds, logos, and other images
  assets/video/          Homepage video
next.config.ts           Next.js settings
eslint.config.mjs        ESLint configuration
postcss.config.mjs       Tailwind PostCSS plugin
tsconfig.json            TypeScript settings and @/* alias
```

## Configuration and customization

No environment variables are required for the current frontend. `next.config.ts` exposes an optional `CUSTOM_API_URL`, but application code does not currently consume it. If an integration needs it, create a local `.env.local` file:

```dotenv
CUSTOM_API_URL=https://api.example.com
```

Values configured through Next.js's `env` option can be included in browser JavaScript. Use this setting only for public configuration, never credentials.

- **Content:** Update the relevant `app/**/page.tsx` file or its components. Jackpot amounts, event information, job listings, and restaurant content are hardcoded.
- **Navigation:** Desktop menus live in `app/components/layout/header.tsx`; mobile menus live in `app/components/layout/navbar.tsx`. Keep both aligned with the route table above.
- **Theme and fonts:** Edit `app/globals.css`. Geist and Geist Mono are configured through `next/font/google` in `app/layout.tsx`; builds need network access to retrieve them.
- **Images and video:** Add assets under `public/` and reference them with root-relative URLs, such as `/assets/images/example.jpg`. Keep filename casing consistent.
- **Preloading:** Update the `criticalImages` list in `app/loading.tsx` when changing important images.
- **Metadata and analytics:** Edit `app/layout.tsx`. It currently includes a hardcoded Google Analytics measurement ID, `G-TXBRCD6JXR`.
- **Imports:** The `@/*` alias resolves from the repository root, for example `@/app/components/layout/layout`.

## Current limitations

- Jackpot amounts and update timestamps are static; no live jackpot feed is connected.
- Contact fields have no submission handler, and the Send link points to `/not-found.tsx`. The newsletter form uses `action="#"` without a subscription service.
- Job application buttons and several tutorial or promotional actions use placeholder destinations such as `/` or `/not-found.tsx`.
- Some mobile submenu URLs do not match implemented routes. Examples include `/gaming/threecard` instead of `/gaming/threeCardGame`, `/dining/epicBar` instead of `/dining/EpicBar`, and `/card-academy/...` instead of `/cardacadamy/...`.
- Some image references need correction. For example, the scroll-to-top control in `app/components/layout/layout.tsx` references a missing `/assets/images/Vector 41.png`.
- The homepage includes an intentional two-second delay in `app/page.tsx`, in addition to the loading overlay.

Before publishing, resolve placeholder links, connect any required services, check assets on a case-sensitive system, and run the checks above. A successful build does not verify that every link or form works.

## Production

```sh
npm ci
npm run build
npm start
```

The build output is written to `.next/`. For a Node.js hosting environment, use `npm run build` as the build command and `npm start` as the start command. The repository does not configure static export.

## License

This project is licensed under the [MIT License](LICENSE), copyright (c) 2025 JamesRubic.
