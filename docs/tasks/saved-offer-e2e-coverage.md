# Saved-offer end-to-end coverage

## Intent and acceptance

Add a browser journey for the existing CAN-08 behavior: saving a public offer persists across reload, remains scoped to the candidate, appears in saved offers, and can be removed with the empty state restored.

`FEATURES.md` was reviewed and needs no update because this change adds test coverage without changing product behavior.

## Verification

- The new browser journey passed with the installed system Chrome: 1 test passed.
- The complete browser suite using system Chrome had 33 passing tests and 2 PDF-download tests fail because Chrome's built-in PDF viewer emits `chrome-extension://` requests that the existing external-request assertions reject. The configured Playwright Chromium executable is not installed, so the standard `npm run test:e2e` could not launch.
- `npm run format:check`, `npm run lint`, `npm test` (27 tests), `npm run verify:packet`, `npm run build`, and `git diff --check` passed.
- `./scripts/verify` stopped at the design-system check because this environment has Node 26.12.1; the check requires Node 24.
- Follow-up: `./scripts/verify` passed under Node 24.22.3 with Playwright-managed Chromium, including all 35 browser journeys and 27 unit tests. The PDF tests passed without modifying their assertions. The build retained its nonblocking Zod annotation and bundle-size warnings.
