# Automation Framework Design

Design varies by 3 inputs: **Framework Type**, **Scope (API/UI)**, **Tool+Language**.

## 1. Framework Type
| Type | Fit |
|---|---|
| Modular | Simple flows |
| Data-Driven | Many data combos, same flow |
| Keyword-Driven | Non-tech stakeholders |
| BDD | Business-readable, traceability |
| **Hybrid (default)** | Modular + Data-Driven + POM/SOM |

## 2. Scope
| Scope | Pattern |
|---|---|
| UI | Page Object Model (POM) |
| API | Service Object Model (SOM) |
| Both | POM + SOM, shared core/utils |

## 3. Tool Matrix
| Tool | Languages | API | UI | Parallel |
|---|---|---|---|---|
| Cypress | JS/TS | `cy.request` | Browser only | CI sharding/Cloud |
| Selenium | Java/Python/C#/Ruby | needs RestAssured/Requests/RestSharp | Widest browser/OS | Grid, TestNG/pytest-xdist |
| Playwright | TS/JS/Java/Python | native `request` | Multi-tab/context/browser | Native workers |

## 4. Structure by Combination

**Cypress (JS/TS)** — UI + light API
```
cypress/{e2e, fixtures, support/pages, support/commands.ts, api}
cypress.config.ts, package.json
```
Deps: cypress, typescript, @cypress/grep, mochawesome.
Notes: `cy.session()` for auth reuse; `cy.request()` for data setup; custom commands = utils layer.

**Selenium (Java/Python/C#/Ruby)** — UI, broad platform coverage
```
src/main/{core, pages, utils, listeners}
src/test/{tests, data}
config/config.{env}.yaml
```
| Lang | Runner | API lib | Report |
|---|---|---|---|
| Java | TestNG/JUnit5 | RestAssured | Allure |
| Python | Pytest | Requests | Allure-pytest |
| C# | NUnit/MSTest | RestSharp | ExtentReports.NET |
| Ruby | RSpec/Cucumber | Faraday | Allure-rspec |
Notes: WebDriverManager for binaries; ThreadLocal driver for parallel; explicit waits only; BaseTest handles setup/teardown+screenshots.

**Playwright (TS/JS/Java/Python)** — UI + API, modern/parallel
```
tests/{ui, api}, pages, services, fixtures, utils, test-data
playwright.config.ts
```
Deps: @playwright/test (TS/JS), pytest-playwright (Python), playwright-java.
Notes: built-in fixtures replace base classes; `request` context = no extra HTTP lib; native parallel workers/contexts; trace viewer (`trace: on-first-retry`) for debugging; multi-browser via `projects[]`.

## 5. Common Core (all combos)
- Config: env-specific files, secrets via env vars/vault
- Reporting: Allure/Extent/native HTML + screenshots/traces on failure
- Tagging: `@smoke`/`@regression`/`@sanity` for CI selection
- CI/CD: build → lint → smoke → regression → report/notify
- Data: externalized JSON/CSV/Excel/DB, no hardcoding
- Retry: only for known transient/flaky failures

## 6. Quick Picks
- Fast local feedback, JS/TS team → **Cypress**
- Broad browser/OS, enterprise, non-JS langs → **Selenium**
- UI+API, speed, native parallelism → **Playwright**
- Need business-readable tests → add BDD layer
- Many data permutations → add data-driven layer

*v1.0 — 2026-08-31*