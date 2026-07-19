# Changelog

All notable changes to this project are documented here, following
[Keep a Changelog](https://keepachangelog.com) and
[Semantic Versioning](https://semver.org).

## [Unreleased]

### Fixed

- Fixed a `TypeError: Cannot read properties of undefined (reading 'length')`
  in `groundY` on first paint. `renderVals()` runs during React's initial
  `render()` — before `componentDidMount()` generates the terrain — and its
  altitude guard checked `this.groundY` (a method, always defined) instead of
  `this.terrain` (the data). It now guards `this.terrain`, matching the method's
  other pre-mount fallbacks.

## [0.1.0] - 2026-07-18

### Added

- Initial versioned release of game-moon-lander.
- In-game version badge sourced from `version.js`.
