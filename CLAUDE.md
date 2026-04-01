# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML landing page ("Coding Plan / 编程计划") for browsing programming study plans. Single `index.html` file with inline CSS and JavaScript. No build tools, frameworks, or package manager.

## Development

Open `index.html` directly in a browser — no server or build step required.

## Architecture

- **index.html** — self-contained page with three sections:
  1. **Inline `<style>`** — tech-green dark theme using CSS variables (documented via comments: `#00e676` primary, `#0a0f0d` background, `#0d1a14` cards, `#69f0ae` highlights, `#1b3a2a` borders). Responsive breakpoints at 768px and 480px.
  2. **HTML body** — navbar, hero with stats, filter bar (beginner/intermediate/advanced), card grid with `data-level` attributes, footer.
  3. **Inline `<script>`** — `filterPlans(level)` toggles card visibility via `display` property and manages active button state.

## Code Style

- Every line of code must have comments (mandatory project convention).
