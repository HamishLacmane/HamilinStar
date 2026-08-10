# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is (currently)

A single placeholder "coming soon" page — no framework, no build step. `index.html` + `styles.css` at the repo root, deploys to GitHub Pages with zero configuration.

## Do not build the real feature yet

Hamilin Star is meant to eventually display "some view of filterable export" of food ratings, but **the data source is explicitly undecided** (Airtable? NocoDB? a static file?) — Hamish deferred this decision (2026-08-09), "will be decided later." Do not build the filterable ratings view, pick a data source, or wire up any backend/API integration until Hamish explicitly settles this. A repo shell existing ahead of time is intentional; a half-built feature guessing at the data source is not.

## Colours are not decided

`styles.css` uses a neutral grey (`--accent: #8A8A8A`) as an explicit placeholder, not a real brand choice. Don't treat it as the final palette or extend it as if it were — Hamish hasn't picked Star's colours yet.

## Content is placeholder — do not write copy

The headline and intro paragraph are literal placeholder text / `TODO(Hamish)` comments. Hamish writes his own site copy; don't fill these in.

## Licence

No LICENSE file by design — all rights reserved by default. Don't add an open-source license without being explicitly asked to change that.
