# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

DPS Technical Inc. website — a static single-page site for a vehicle sound control and compliance testing company. No build tools, no frameworks, no package manager.

## Architecture

Everything lives in a single `index.html` file:
- **Lines 15–832**: Embedded `<style>` block (all CSS)
- **Lines 834–1088**: HTML content (nav, hero, 5 service sections, contact, footer)
- **Lines 1090–1143**: Embedded `<script>` block (all JS, wrapped in IIFE)

There are no external JS/CSS files. The only external dependency is Google Fonts (Barlow, Barlow Condensed).

## Development

No build step. Open `index.html` in a browser to preview. Any local HTTP server works (e.g., `python3 -m http.server`).

## Deployment

Automated via GitHub Actions (`.github/workflows/deploy.yml`). Pushing to `main` triggers FTP deployment to GoDaddy hosting using `SamKirkland/FTP-Deploy-Action@v4.3.5`. FTP credentials are stored in GitHub Secrets (`FTP_SERVER`, `FTP_USERNAME`, `FTP_PASSWORD`).

## Design System

CSS custom properties defined in `:root`:
- `--yellow: #FFE000` (accent/CTA)
- `--red: #E02020` (secondary accent, labels)
- `--black: #0A0A0A`, `--dark: #111111`, `--dark-surface: #1A1A1A` (backgrounds)
- `--gray: #888888` (body text), `--light: #E8E8E8` (emphasis text), `--white: #FFFFFF` (headings)

Typography: `'Barlow'` for body text, `'Barlow Condensed'` for headings/labels/UI. Fluid sizing via `clamp()`.

Single responsive breakpoint at `640px`.

## Key Conventions

- CSS class naming is semantic/component-based: `.service-card`, `.card-title`, `.highlight-box`
- Card variants use modifier classes: `.featured`, `.coming-soon`
- Service sections alternate backgrounds via `:nth-child(odd/even)`
- Navigation visibility is controlled by `IntersectionObserver` watching the hero section
- Mobile nav uses `.open` class toggle on both `.nav-toggle` and `.nav-links`
