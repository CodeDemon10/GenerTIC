# Smart Contract Auditor

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](#)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)
[![Coverage](https://img.shields.io/badge/coverage---%25-yellowgreen.svg)](#)

## Overview

**Smart Contract Auditor** is a developer-friendly toolkit and CLI for performing automated security audits on Ethereum-compatible smart contracts. It combines static analysis, symbolic checks, automated test scaffolding, and a human-readable findings report template so teams can integrate security scanning into CI/CD and developer workflows.

This repository contains:

* A modular CLI auditor to run analyzers and tests.
* Pre-built analyzers for common vulnerabilities (reentrancy, integer overflow, access control, uninitialized variables, gas consumption hotspots, etc.).
* Templates for audit reports and remediation steps.
* CI examples to run scans on pull requests.

---

## Features

* Static analysis (pattern checks + AST rules)
* Symbolic/taint-style detectors for reentrancy and cross-function issues
* Fuzz / property-based test scaffolding with example harnesses
* Gas & complexity heuristics
* Audit report generator (JSON + Markdown)
* Configurable rule set and severity levels
* GitHub Actions and pre-commit hooks examples

---

## Quick start

### Requirements

* Node.js >= 18 (or the Node version your tooling uses)
* npm or yarn
* Python 3.10+ (optional — for some analyzers)
* Hardhat or Foundry installed for running tests (examples provided)

### Install

```bash
git clone <your-repo-url>
cd smart-contract-auditor
# install node deps
npm install
# or
# yarn install
```

### Run a basic audit (example)

```bash
# run CLI against a folder of contracts
npm run audit -- --contracts ./contracts --output ./reports

# or, if using npx
npx smart-auditor --contracts ./contracts --output ./reports
```

This will run the default analyzers and write a `report.json` and a `report.md` under `./reports`.

---

## CLI usage

```text
Usage: smart-auditor [options]

Options:
  --contracts <path>       Path to solidity contracts folder (required)
  --config <file>          Path to auditor config file (default: auditor.config.json)
  --output <dir>           Output directory for reports (default: ./reports)
  --format <json|md|both>  Output format (default: both)
  --rules <list>           Comma-separated list of analyzer rules to run
  --ci                     Run in CI mode (non-interactive)
  -h, --help               display help for command
```

---

## Configuration

Create an `auditor.config.json` in the project root to control rule severities, disabled checks, and report formatting. Example:

```json
{
  "severity": {
    "reentrancy": "high",
    "overflow": "medium",
    "access_control": "high"
  },
  "disabled_rules": ["naming_conventions"],
  "report": {
    "include_stack_traces": true,
    "format": "both"
  }
}
```

---

## Audit report

The auditor produces two files per run:

1. `report.json` — machine readable, includes findings with rule id, severity, file:/line, proof / evidence, and suggested remediation.
2. `report.md` — human-friendly summary, recommended for sharing with stakeholders.

### Example finding (markdown snippet)

```md
### HIGH — Reentrancy in `Vault.sol:withdraw`
**Location:** `contracts/Vault.sol:234-276`
**Description:** External call performed before state update allows attacker to re-enter `withdraw` and drain funds.
**Evidence:** call to `msg.sender.call.value(amount)()` inside withdraw before `balances[msg.sender] = 0`.
**Remediation:** Move state update before external call; use `transfer()`/`send()` or a pull-pattern; add reentrancy guard.
```

---

## Integrating with CI (GitHub Actions example)

Create `.github/workflows/audit.yml`:

```yaml
name: Smart Contract Audit
on: [pull_request]

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 18
      - run: npm ci
      - run: npm run audit -- --contracts ./contracts --output ./reports --ci
      - name: Upload report
        uses: actions/upload-artifact@v4
        with:
          name: audit-reports
          path: ./reports
```

This will run the automated audit on every PR and upload the reports for reviewers.

---

## Recommended manual review checklist

Automated tools help, but manual review is essential. Each audit should include:

1. Design review: check tokenomics, access control, upgradeability surface.
2. Critical function review: `mint`, `burn`, `pause`, `upgrade`, `admin` flows.
3. State-change ordering checks (reentrancy, checks-effects-interactions)
4. Gas & DoS by block gas limit checks
5. Initialization/constructor and proxy patterns
6. Dependency & external call trust boundaries

---

## Contributing

Contributions welcome! Please follow these steps to propose a change:

1. Fork the repo and create a feature branch (`git checkout -b feat/<name>`)
2. Add tests and a changelog entry for any new analyzer or major change
3. Submit a pull request with a clear description of what you added and why

Please sign the Contributor License Agreement (CLA) if requested by repository owners.

---

## License

This project is released under the **MIT License**. See `LICENSE` for full text.

---

## Contact / Authors

Created and maintained by the Smart Contract Auditor team.

For security-sensitive disclosures, please use our private disclosure channel: `security@example.com` (replace with your contact email) and encrypt with our PGP key (available in `./pgp-key.asc`).

---

## Templates & Extras

* `AUDIT_TEMPLATE.md` — ready-to-fill audit report for manual audits
* `ISSUE_TEMPLATES/security.md` — GitHub issue template for security reports
* Example `foundry` / `hardhat` scripts under `examples/` to run property tests and gas profiling

---

*Happy auditing — keep contracts secure!*
