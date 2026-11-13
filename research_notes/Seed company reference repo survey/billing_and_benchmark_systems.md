# Open-source billing/subscription/notification platforms and research microservice benchmarks (state as of 2026-11-11)

Method note for the report writer. Repository metadata (stars, licence SPDX id, archived flag, last push, primary language, size) was read from the GitHub REST API (`api.github.com/repos/<owner>/<repo>`) on 2026-11-11; "size" is GitHub's repository size in KB (git data, not lines of code). Licence texts, READMEs, OpenAPI files and docs pages were read directly (raw files or the vendor's Markdown docs). The GitHub API rate limit was hit part-way through, so a second group of repositories has licence/archived status read from the repo HTML page but **no verified star count**; these are marked "stars not verified". Web search was unavailable for most of the session, so the "others not on the list" discovery relied on direct repository probes and one arXiv API title query, not a broad search.

## 1. Inventory: repository URL, licence, stars, maintenance, language, size

### Takeaway
The permissively licensed, actively maintained references are Kill Bill (Apache-2.0, Java), Hyperswitch (Apache-2.0, Rust), OpenMeter (Apache-2.0, Go), Polar (Apache-2.0, Python), Saleor (BSD-3), eShop (MIT, C#), Notifo (MIT, C#) and the Online Boutique / OpenTelemetry demo apps (Apache-2.0); Lago, Flexprice, Meteroid and listmonk are AGPL-3.0 and Vendure is GPLv3 (read-only for us). Two licence anomalies need care: DeathStarBench's LICENSE file is Apache-2.0 but its README says GPL v2, and µBench is BSD 4-Clause (advertising clause), which GitHub reports as "NOASSERTION".

### Cited Findings

Billing / subscription / payments / commerce (GitHub API, 2026-11-11):

| System | Repo | Licence (exact) | Stars | Last push | Primary lang | Size (KB) | Status |
|---|---|---|---|---|---|---|---|
| Lago (monorepo/umbrella) | https://github.com/getlago/lago | AGPL-3.0 (LICENSE file and README badge agree) | 10,795 | 2026-11-09 | Go (as reported by GitHub) | 156,909 | active |
| Lago API | https://github.com/getlago/lago-api | AGPL-3.0 | 443 | 2026-11-11 | Ruby | 63,035 | active |
| Kill Bill | https://github.com/killbill/killbill | Apache-2.0 | 5,852 | 2026-11-12 UTC | Java | 682,778 | active (created 2012) |
| Hyperswitch | https://github.com/juspay/hyperswitch | Apache-2.0 | 45,763 | 2026-11-12 UTC | Rust | 491,224 | active |
| OpenMeter | https://github.com/openmeterio/openmeter | Apache-2.0 | 2,442 | 2026-11-12 UTC | Go | 142,364 | active; README says releases are beta |
| Flexprice | https://github.com/flexprice/flexprice | AGPL-3.0, open core | 6,873 | 2026-11-12 UTC | Go | 247,793 | active (created 2024-11) |
| Meteroid | https://github.com/meteroid-oss/meteroid | AGPL-3.0 + enterprise edition | 1,358 | 2026-11-06 | Rust | 47,909 | active |
| Polar | https://github.com/polarsource/polar | Apache-2.0 | 10,471 | 2026-11-12 UTC | Python | 574,977 | active |
| Medusa | https://github.com/medusajs/medusa | MIT except Enterprise Edition materials (GitHub: NOASSERTION) | 37,195 | 2026-11-11 | TypeScript | 902,738 | active |
| Saleor | https://github.com/saleor/saleor | BSD-3-Clause | 23,555 | 2026-11-10 | Python | 248,671 | active |
| Vendure | https://github.com/vendurehq/vendure (moved from vendure-ecommerce/vendure) | Dual: GPLv3 or Vendure Commercial License | not verified | not verified | TypeScript (per repo title) | n/a | active per README |
| eShop (.NET reference app) | https://github.com/dotnet/eShop | MIT | 11,017 | 2026-11-09 | C# | 27,430 | active |

- All rows above except Vendure: [GitHub API](https://api.github.com/repos/killbill/killbill) (same endpoint pattern per repo).
- Lago's README carries an "AGPLv3" badge and the LICENSE file is the GNU AGPL v3 text; no discrepancy found. The README now positions Lago as "Agentic-first monetization infrastructure for AI products". — [Lago README](https://raw.githubusercontent.com/getlago/lago/main/README.md), [Lago LICENSE](https://raw.githubusercontent.com/getlago/lago/main/LICENSE)
- Some Lago features are premium/licence-gated even self-hosted: manual credit-note creation ("only users with a premium license can manually generate credit notes") and automatic dunning ("PREMIUM ADD-ON ... available upon request only"). — [Lago credit notes](https://getlago.com/docs/guide/invoicing/credit-notes/overview.md), [Lago automatic dunning](https://getlago.com/docs/guide/dunning/automatic-dunning.md)
- Kill Bill README: "free to use and completely open-source under the Apache License 2.0"; "Aviate is the enterprise version of Kill Bill" under a commercial licence. — [Kill Bill README](https://raw.githubusercontent.com/killbill/killbill/master/README.md)
- Medusa's LICENSE opens: "Except for the Enterprise Edition materials identified in ENTERPRISE-LICENSE.md, the repository is licensed under the MIT License below." — [Medusa LICENSE](https://raw.githubusercontent.com/medusajs/medusa/develop/LICENSE)
- Vendure LICENSE.md: "available under two different licenses: GNU General Public License version 3 (GPLv3) as Vendure Community Edition; Vendure Commercial License (VCL)", with a GPL section-7 plugin exception. README adds that "Building against the GraphQL API doesn't make your storefront or services subject to GPLv3". The old `vendure-ecommerce/vendure` API path returns "Moved Permanently". — [Vendure LICENSE.md](https://raw.githubusercontent.com/vendurehq/vendure/master/LICENSE.md), [Vendure README](https://raw.githubusercontent.com/vendurehq/vendure/master/README.md)
- Flexprice README: "Open Core" where the core "(99%) is fully open source, licensed under AGPLv3" and some parts require a commercial licence. — [Flexprice README](https://raw.githubusercontent.com/flexprice/flexprice/main/README.md)
- Meteroid README: repository code and `meteroid-oss-*` images are AGPL V3; "The default images, Meteroid Enterprise, are licensed under the Meteroid Enterprise License". — [Meteroid README](https://raw.githubusercontent.com/meteroid-oss/meteroid/main/README.md)
- Polar README: "Licensed under Apache License, Version 2.0". — [Polar README](https://raw.githubusercontent.com/polarsource/polar/main/README.md)
- OpenMeter README: "Releases are beta and can include breaking changes"; it is "not ... a bundled operator UI, payment processor, tax engine, or general-purpose accounting system". — [OpenMeter README](https://raw.githubusercontent.com/openmeterio/openmeter/main/README.md)

Notification infrastructure (GitHub API, 2026-11-11):

| System | Repo | Licence | Stars | Last push | Lang | Size (KB) |
|---|---|---|---|---|---|---|
| Novu | https://github.com/novuhq/novu | MIT core + proprietary `enterprise/` (GitHub: NOASSERTION) | 40,324 | 2026-11-12 UTC | TypeScript | 529,747 |
| listmonk | https://github.com/knadh/listmonk | AGPL-3.0 | 24,258 | 2026-11-12 UTC | Go | 55,411 |
| Apprise | https://github.com/caronc/apprise | BSD-2-Clause | 17,753 | 2026-11-11 | Python | 18,126 |
| Notifo | https://github.com/notifo-io/notifo | MIT | 885 | 2026-09-20 | C# | 27,048 |

- Rows: [GitHub API](https://api.github.com/repos/novuhq/novu).
- Novu ships three licence files (`LICENSE-MIT`, `LICENSE-ENTERPRISE`, `EE-PACKAGES-LICENSE`); README states "the core technology is fully open source, licensed under MIT license, and the enterprise code is covered under a commercial license". LICENSE-ENTERPRISE says content under `enterprise/packages` is under EE-PACKAGES-LICENSE and "Content outside of the above mentioned directories ... is available under the 'MIT' license". Default branch is `next`. — [Novu repo](https://github.com/novuhq/novu), [LICENSE-ENTERPRISE](https://raw.githubusercontent.com/novuhq/novu/next/LICENSE-ENTERPRISE)

Research benchmarks, demo apps and datasets (GitHub API, 2026-11-11):

| System | Repo | Licence | Stars | Last push | Lang | Size (KB) | Status |
|---|---|---|---|---|---|---|---|
| Train Ticket | https://github.com/FudanSELab/train-ticket | Apache-2.0 | 927 | 2025-11-21 | Java | 82,675 | not archived; about a year since last push |
| DeathStarBench | https://github.com/delimitrou/DeathStarBench | **LICENSE file: Apache-2.0; README: GPL v2** | 965 | 2024-07-09 | Lua (GitHub's label) | 134,928 | not archived; dormant since mid-2024 |
| TeaStore | https://github.com/DescartesResearch/TeaStore | Apache-2.0 | 167 | 2025-01-08 | Java | 107,367 | not archived; low activity |
| µBench | https://github.com/mSvcBench/muBench | BSD 4-Clause (GitHub: NOASSERTION) | 84 | 2025-06-12 | Python | 14,543 | low activity |
| Alibaba cluster traces | https://github.com/alibaba/clusterdata | no licence detected | 2,258 | 2026-10-13 | Jupyter Notebook | 41,064 | active |
| RCAEval | https://github.com/phamquiluan/RCAEval | MIT (bundled baselines have mixed licences) | 265 | 2026-11-06 | Python | 4,766 | active |
| Online Boutique | https://github.com/GoogleCloudPlatform/microservices-demo | Apache-2.0 | 21,179 | 2026-10-27 | Go | 38,292 | active |
| Sock Shop | https://github.com/microservices-demo/microservices-demo | Apache-2.0 | 3,779 | 2023-12-05 | Python | 54,219 | **archived** |
| OpenTelemetry Demo | https://github.com/open-telemetry/opentelemetry-demo | Apache-2.0 | 3,449 | 2026-11-10 | TypeScript | 61,409 | active |
| GAIA dataset | https://github.com/CloudWise-OpenSource/GAIA-DataSet | GPL-2.0 | 286 | 2023-06-16 | none | 7,809,649 | dormant |
| Nezha | https://github.com/IntelligentDDS/Nezha | MIT | 80 | 2025-05-20 | Python | 342,975 | low activity |

- Rows: [GitHub API](https://api.github.com/repos/FudanSELab/train-ticket).
- DeathStarBench licence discrepancy: the LICENSE file is "Apache License Version 2.0", while the README says "DeathStarBench is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, version 2." — [DSB LICENSE](https://raw.githubusercontent.com/delimitrou/DeathStarBench/master/LICENSE); contradicted by [DSB README](https://raw.githubusercontent.com/delimitrou/DeathStarBench/master/README.md)
- µBench LICENSE is "BSD 4-Clause License, Copyright (c) 2021, University of Rome Tor Vergata", including the advertising-acknowledgement clause. — [µBench LICENSE](https://raw.githubusercontent.com/mSvcBench/muBench/main/LICENSE)
- RCAEval: "This repository includes code from various sources with different licenses"; two bundled baselines (CausalRCA, RUN) are listed as "No License". — [RCAEval README](https://raw.githubusercontent.com/phamquiluan/RCAEval/main/README.md)
- Train Ticket README: "contains 41 microservices", languages Java (Spring Boot/Cloud), Node.js (Express), Python (Django), Go (Webgo), DBs Mongo and MySQL. — [Train Ticket README](https://raw.githubusercontent.com/FudanSELab/train-ticket/master/README.md)

Found beyond the suggested list, licence read from the repo page, **stars not verified** (API rate-limited):
- OpenRCA (ICLR'25, "Can Large Language Models Locate the Root Cause of Software Failures"), MIT. — [microsoft/OpenRCA](https://github.com/microsoft/OpenRCA)
- AIOpsLab ("holistic framework to enable the design, development, and evaluation of autonomous AIOps agents"), MIT. — [microsoft/AIOpsLab](https://github.com/microsoft/AIOpsLab)
- ITBench ("open source benchmarking framework for IT automation"), Apache-2.0. — [itbench-hub/ITBench](https://github.com/itbench-hub/ITBench)
- SREGym ("Can AI agents resolve production incidents?"); the URL `xlab-uiuc/SREGym` resolves to a repo titled `xlab-uiuc/SREGym-REU`; licence not detected. — [xlab-uiuc/SREGym](https://github.com/xlab-uiuc/SREGym)
- Aegis ("a platform for root-cause-analysis research on microservice systems"), Apache-2.0. — [OperationsPAI/aegis](https://github.com/OperationsPAI/aegis)
- Online Marketplace benchmark (data management in microservices); `diku-dk/EventBenchmark` now resolves to `diku-dk/OnlineMarketplaceBenchmark`; licence not detected. — [repo](https://github.com/diku-dk/EventBenchmark), [paper arXiv:2403.12605](http://arxiv.org/abs/2403.12605v4)
- eShopOnContainers (older .NET microservices sample) is **archived**; `dotnet/eShop` is its live successor in this inventory. — [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers)
- Svix webhooks service ("open source and enterprise-ready webhooks service"), MIT. — [svix/svix-webhooks](https://github.com/svix/svix-webhooks)
- Lotus ("Open Source Pricing & Packaging Infrastructure"), MIT per repo page; maintenance status not verified. — [uselotus/lotus](https://github.com/uselotus/lotus)
- Recent arXiv benchmark papers surfaced by a title query: MicroRemed (2025-11, LLM remediation via Ansible playbooks) [arXiv:2511.01166](http://arxiv.org/abs/2511.01166v1); "Rethinking the Evaluation of Microservice RCA with a Fault Propagation-Aware Benchmark" (2025-10) [arXiv:2510.04711](http://arxiv.org/abs/2510.04711v2); RepoGenesis (2026-01, 106 repos, 1,258 API endpoints, README-to-repository microservice generation) [arXiv:2601.13943](http://arxiv.org/abs/2601.13943v3); "A Multi-Dataset Benchmark for Evaluating LLM Agents in Microservice Failure Diagnosis" (2026-06, AIOps2025 and RCA100, 500+ cases on HipsterShop and OpenTelemetry Demo) [arXiv:2606.29193](http://arxiv.org/abs/2606.29193v1); MicroServo scenario-oriented AIOps benchmark (2024-07) [arXiv:2407.14532](http://arxiv.org/abs/2407.14532v1).

### Inferences
- For a seed company whose code must be original, the safe "read and imitate structure" set is the Apache/MIT/BSD group; Lago, Flexprice, Meteroid, listmonk (AGPL) and Vendure (GPLv3) should be used for concepts and public API contracts only. Lago's OpenAPI file lives in a separate repo (`getlago/lago-openapi`) whose own licence I did not verify.
- DeathStarBench should be treated as licence-ambiguous (GPL v2 per README vs Apache-2.0 per LICENSE) until resolved; do not copy code from it.
- GitHub's "language" for `getlago/lago` (Go) and DeathStarBench (Lua) reflects byte counts of the umbrella repo, not the main implementation language; Lago's API is Ruby (`lago-api`).

### Gaps
- Star counts and last-push dates for Vendure, OpenRCA, AIOpsLab, ITBench, SREGym, Aegis, Online Marketplace, Svix, Lotus, ntfy, Robot Shop, chaos-mesh were not obtained (GitHub API rate limit).
- Lines-of-code sizes were not measured; only GitHub repo size in KB.
- Licence of `getlago/lago-openapi`, `killbill/killbill-docs` and `FudanSELab/train-ticket-fault-replicate` not verified.
- Alibaba `clusterdata` has no licence file that GitHub detects; usage terms beyond "cite our paper" and survey-gated downloads were not found.
- I did not verify any relicensing history (e.g. whether any of these changed licence in 2025-2026); only the current state was read.

## 2. Billing domain: core entities and rules, and which rules cross a service boundary

### Takeaway
Kill Bill and Lago document the same core model from two angles: catalog (product/plan/phase/price) → subscription → invoice (typed line items) → payment, with credits, refunds, proration, overdue/dunning and entitlement as separately stated rules. The rules that other services must agree with are: integer minor-unit amounts plus currency, the subscription and invoice state enums, the entitlement-versus-billing distinction, upgrade/downgrade timing, dedup keys for usage and webhooks, and the order of applying coupons, tax and credits.

### Cited Findings

Kill Bill (Apache-2.0):
- Entities: Account (payment methods, balance, tags); Bundle (at most one BASE subscription plus several ADD_ON); Subscription (plan + start date, tracks charge-through date); Catalog (versioned by `effectiveDate`); Product (BASE, ADD_ON, STANDALONE); Plan made of Phases (TRIAL, DISCOUNT, FIXEDTERM, EVERGREEN); Price List (DEFAULT required). — [Kill Bill subscription guide](https://docs.killbill.io/latest/userguide_subscription)
- Billing rules: billing periods DAILY to BIENNIAL; bill cycle day (BCD), and a BCD past month end moves to the month's last day; billing alignment ACCOUNT / SUBSCRIPTION / BUNDLE; recurring billed in advance, usage IN_ARREAR. — [Kill Bill subscription guide](https://docs.killbill.io/latest/userguide_subscription)
- Proration: initial bill prorated when BCD differs from start date; plan changes produce a `REPAIR_ADJ` item for the unused part of the old plan. — [same](https://docs.killbill.io/latest/userguide_subscription)
- Plan change timing policy: END_OF_TERM, IMMEDIATE or ILLEGAL; cancellation END_OF_TERM (no credit) or IMMEDIATE (credits unused balance); rules are ordered cases, first match wins. — [same](https://docs.killbill.io/latest/userguide_subscription)
- Entitlement and billing are separate and "not necessarily aligned" (access can end immediately while billing runs to the end of the paid period). — [same](https://docs.killbill.io/latest/userguide_subscription)
- Invoice item types: RECURRING, FIXED, EXTERNAL_CHARGE, USAGE, TAX (charges); ITEM_ADJ, CREDIT_ADJ, REPAIR_ADJ (negative); CBA_ADJ (account credit balance, positive when generated, negative when consumed). Balance is zero for WRITTEN_OFF or DRAFT invoices. — [same](https://docs.killbill.io/latest/userguide_subscription)
- Payments and refunds: one payment normally pays one invoice; partial payments allowed but one payment cannot cover several invoices; refund is a negative payment entry often paired with ITEM_ADJ; chargeback recorded as CHARGED_BACK; auto-pay blocked by AUTO_PAY_OFF or MANUAL_PAY tags. — [same](https://docs.killbill.io/latest/userguide_subscription)
- Overdue (dunning): state is per account; conditions are unpaid invoice count, total unpaid balance, time since earliest unpaid invoice, control tags; actions are `subscriptionCancellationPolicy` (NONE/IMMEDIATE/END_OF_TERM), `blockChanges`, `disableEntitlementAndChangesBlocked`; failed payment retries default to 8 days apart, three times; plugin failure retries once after 300 seconds. — [same](https://docs.killbill.io/latest/userguide_subscription)
- Currency: catalog lists supported currencies and every recurring/fixed price needs a value in each. — [same](https://docs.killbill.io/latest/userguide_subscription)

Lago (AGPL-3.0; concepts and public API only), from its OpenAPI 3.1.0 spec, API version 1.57.0:
- Invoice fields are integer cents plus a currency: `fees_amount_cents`, `coupons_amount_cents`, `credit_notes_amount_cents`, `sub_total_excluding_taxes_amount_cents`, `taxes_amount_cents`, `sub_total_including_taxes_amount_cents`, `prepaid_credit_amount_cents`, `progressive_billing_credit_amount_cents`, `total_amount_cents`, `total_paid_amount_cents`, `total_due_amount_cents`; plus `payment_due_date`, `payment_overdue` (boolean), `net_payment_term`, `version_number`. — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Enums: invoice `status` = draft, finalized, voided, failed, pending, deleted; invoice `payment_status` = pending, succeeded, failed; `invoice_type` = subscription, add_on, credit, one_off, advance_charges, progressive_billing. — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Subscription: `external_id`, `external_customer_id`, `plan_code`, `billing_time` (calendar | anniversary), `status` (active, canceled, incomplete, pending, terminated), `previous_plan_code`, `next_plan_code`, `downgrade_plan_date`, `trial_ended_at`, `current_billing_period_started_at/ending_at`, `on_termination_credit_note` (credit, refund, offset, skip), `on_termination_invoice` (generate, skip), `cancellation_reason` (payment_failed, timeout, manual). — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Rounding: fees and credit notes carry both integer cents and string "precise" amounts (`amount_cents` and `precise_amount`, `taxes_precise_amount`, `precise_unit_amount`, `precise_total_amount_cents`, `precise_coupons_amount_cents`); billable metrics have `rounding_function` and `rounding_precision` ("Number of decimal places kept when `rounding_function` is applied. It can be a positive or negative value, and it defaults to 0"). — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Credit notes: `credit_status` (available, consumed, voided), `refund_status` (pending, succeeded, failed), `reason` (duplicated_charge, product_unsatisfactory, order_change, order_cancellation, fraudulent_charge, other), and separate `credit_amount_cents`, `refund_amount_cents`, `offset_amount_cents`, `balance_amount_cents`. — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Credit note rules: only for invoices with status `finalized` and amount greater than zero; methods are credit for future use, refund the paid amount, or offset the amount due; on subscription invoices "prepaid credits and applied credit notes cannot be refunded"; "Coupons are non-refundable and cannot be credited back". — [Lago credit notes](https://getlago.com/docs/guide/invoicing/credit-notes/overview.md)
- Order of application: "coupons apply before tax and credit notes, then prepaid credits, after tax". — [Lago llms.txt index](https://getlago.com/llms.txt)
- Upgrade/downgrade: plans are compared by yearly amount (monthly ×12, quarterly ×4, semiannual ×2, weekly ×52). Upgrade (new ≥ old) applies immediately; paid-in-advance gets a credit note for unused days; paid-in-arrears gets an immediate prorated invoice for the old plan. Worked example: €100/month Plan A from Jan 1, upgraded to €200/month Plan B on Jan 15 → €45.16 (14/31 × €100) on Jan 15 and €109.68 (17/31 × €200) on Jan 31. Downgrade applies at the end of the current period; the new plan stays `pending` until then. — [Lago upgrades and downgrades](https://getlago.com/docs/guide/subscriptions/upgrades-downgrades.md)
- Dunning campaign: overdue-balance threshold per currency, delay between attempts in days, number of attempts; ends when the overdue balance is paid or attempts are exhausted; a customer whose invoiced currency is not in the campaign is not eligible. — [Lago automatic dunning](https://getlago.com/docs/guide/dunning/automatic-dunning.md)
- Usage metering: aggregations COUNT, SUM, MAX, UNIQUE COUNT, CUSTOM; usage event requires `transaction_id`, `external_subscription_id`, `code`, with optional `timestamp`, `properties`, `precise_total_amount_cents`. — [Lago llms.txt](https://getlago.com/llms.txt), [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Entitlement boundary stated explicitly: "Lago supplies commercial state; the customer's application or gateway performs request-path enforcement ... Do not claim Lago natively blocks requests at quota." — [Lago llms.txt](https://getlago.com/llms.txt)
- Wallet (prepaid credits): `rate_amount`, `credits_balance`, `balance_cents`, `ongoing_balance_cents`, `status` (active, terminated), `expiration_at`, `recurring_transaction_rules`. — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)

Vendor practice (Stripe, used as description of practice):
- Proration example: upgrading from a 10 USD to a 20 USD monthly plan halfway through the period bills an additional 5 USD; "Negative prorations aren't automatically refunded and positive prorations aren't immediately billed". — [Stripe prorations](https://docs.stripe.com/billing/subscriptions/prorations.md)
- Idempotency: `Idempotency-Key` header; keys up to 255 characters; v1 saves the status code and body of the first request "including 500 errors"; keys may be pruned after at least 24 hours; "compares incoming parameters to those of the original request and errors if they're not the same"; results are not saved if validation fails or a concurrent request conflicts; all POST requests accept keys, GET and DELETE do not need them. — [Stripe idempotent requests](https://docs.stripe.com/api/idempotent_requests)

OpenMeter (Apache-2.0):
- Capabilities: ingest CloudEvents and aggregate usage; versioned plans, features, add-ons with flat, per-unit, tiered, package or dynamic prices; entitlements with "feature access and usage-limit balances for your application to enforce"; invoice lifecycle and customer credit balances. — [OpenMeter README](https://raw.githubusercontent.com/openmeterio/openmeter/main/README.md)

### Inferences
- Rules that cross a service boundary in a four-service seed company (my synthesis from the documented contracts, not stated by any one source):
  1. Money representation: integer minor units plus ISO currency in every payload (Lago `*_amount_cents` + `currency`); the rounding rule for proration (Lago's 14/31 × €100 = €45.16 implies day-count proration rounded to cents) must be identical in Storefront price display, Orders totals and Billing invoices.
  2. State enums: subscription status and invoice status/payment_status are consumed by Orders (fulfilment gating), Storefront (account page) and Notifications (template choice). Adding or renaming an enum value is a cross-service change.
  3. Entitlement vs billing: Kill Bill and Lago both keep "may the customer use it" separate from "what is owed"; Orders/Storefront enforce, Billing only reports. Overdue state blocking entitlement (Kill Bill `disableEntitlementAndChangesBlocked`) is a rule both sides must agree on.
  4. Plan change timing (upgrade immediate, downgrade end-of-period) and cancellation policy (immediate with credit vs end-of-term) determine what Orders ships next cycle and what Notifications says.
  5. Order of deductions: coupon before tax, credits after tax; changing it in Billing silently changes totals shown elsewhere.
  6. Identity and dedup keys: `external_id` / `external_customer_id` are owned by the caller, not Billing; usage `transaction_id` and webhook unique key define replay behaviour.
  7. Refund semantics: credit vs refund vs offset are distinct outcomes; Orders must not treat a credit note as cash returned.
- Kill Bill's typed invoice items (RECURRING, FIXED, USAGE, TAX, REPAIR_ADJ, CBA_ADJ, ITEM_ADJ, CREDIT_ADJ) are a compact, permissively licensed vocabulary that a small C# Billing service could imitate.

### Gaps
- Kill Bill's rounding rules are not described in the subscription guide I read; its entitlement state names (e.g. ENT_STARTED/ENT_BLOCKED) were not confirmed on that page.
- Tax engine rules (inclusive vs exclusive, per-line vs per-invoice rounding) were not verified for any system; Lago only shows `taxes_amount_cents`, `taxes_rate`, `applied_taxes` fields and mentions Anrok/Avalara integrations.
- Lago's grace-period and overdue pages were not read (URL moved to `/docs/guide/invoicing/invoicing-settings/grace-period.md`).
- Hyperswitch, Polar, Flexprice, Meteroid, Medusa, Saleor and Vendure domain models were not examined in depth.
- Multi-currency conversion rules were not found in any source read.

## 3. External contracts: REST/OpenAPI, webhook/event catalogues, payload fields, idempotency, versioning

### Takeaway
Two contract styles are documented: "fat" events that embed the object (Lago: `webhook_type` + `object_type` + embedded object; Hyperswitch: `event_type` + `content`) and "thin" events that carry only ids (Kill Bill: `eventType`, `objectType`, `objectId`, `accountId`; Stripe now recommends thin events to avoid payload versioning). All of them specify at-least-once delivery with retries and expect the consumer to deduplicate by an event id or unique-key header.

### Cited Findings

Lago:
- OpenAPI 3.1.0, API version 1.57.0, servers `https://api.getlago.com/api/v1` (US) and `https://api.eu.getlago.com/api/v1`; a single file of about 1.1 MB with a top-level `webhooks:` section that defines each message with its headers and body schema. — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Envelope: `{"webhook_type": "__TYPE__", "object_type": "__OBJECT_TYPE__", "organization_id": "...", "__OBJECT_TYPE__": {}}`; "an `invoice.created` message has `"object_type": "invoice"` and an `invoice` key". — [Lago webhook format](https://getlago.com/docs/api-reference/webhooks/format---signature.md)
- Delivery: non-2xx or network failure → resent; "Lago attempts each message 3 times, waiting longer between each attempt". Headers: `X-Lago-Unique-Key` ("idempotency key ... Use it to process a message only once"), `X-Lago-Signature`, `X-Lago-Signature-Algorithm` (`jwt` RS256, the default, or `hmac` = Base64 HMAC-SHA256 of the payload). — [Lago webhook format](https://getlago.com/docs/api-reference/webhooks/format---signature.md), [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Event catalogue (verbatim names, selection): `invoice.drafted`, `invoice.ready_to_finalize`, `invoice.created` (finalized), `invoice.one_off_created`, `invoice.paid_credit_added`, `invoice.generated` (PDF), `invoice.payment_status_updated`, `invoice.payment_overdue`, `invoice.voided`, `invoice.payment_failure`, `invoice.payment_dispute_lost`; `subscription.incomplete`, `subscription.started`, `subscription.updated`, `subscription.termination_alert` (45 and 15 days before end), `subscription.terminated`, `subscription.canceled`, `subscription.trial_ended`, `subscription.usage_threshold_reached`; `credit_note.created`, `credit_note.generated`, `credit_note.refund_failure`; `payment.requires_action`, `payment.succeeded`, `payment_request.created`, `payment_request.payment_failure`; `dunning_campaign.finished`; `wallet.depleted_ongoing_balance`, `wallet_transaction.created/updated/payment_failure`; `fee.created`; `customer.created/updated`; `alert.triggered/resolved`; `events.errors`. — [Lago webhook messages](https://getlago.com/docs/api-reference/webhooks/messages)
- Deprecation example: `event.error` is marked deprecated in favour of the hourly `events.errors`; the page tells integrators to accept unknown event types because new types are added over time. — [Lago webhook messages](https://getlago.com/docs/api-reference/webhooks/messages)
- Plan change is signalled as two messages: `subscription.terminated` for the old plan with `next_plan_code`, then `subscription.started` for the new plan with `previous_plan_code`; `subscription.external_id` persists across both. — [Lago upgrades and downgrades](https://getlago.com/docs/guide/subscriptions/upgrades-downgrades.md)
- Usage-event dedup differs by storage backend: Postgres store key = `transaction_id` + `external_subscription_id`, repeat is rejected with `422` (`value_already_exist`), first copy billed; ClickHouse store key = `transaction_id` + `timestamp` + `external_subscription_id` + `code`, repeat accepted with `200`, latest copy replaces the earlier one. Dedup works across REST and Kafka ingestion. — [Lago ingesting usage](https://getlago.com/docs/guide/events/ingesting-usage.md)
- Subscription `external_id` "serves as an idempotency key, ensuring that each subscription is unique". — [Lago OpenAPI](https://raw.githubusercontent.com/getlago/lago-openapi/main/openapi.yaml)
- Rate limiting: `429` with `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`; retry is safe only if the identical payload including timestamp is resent. — [Lago ingesting usage](https://getlago.com/docs/guide/events/ingesting-usage.md)

Kill Bill:
- Event object (`ExtBusEvent`) fields: `eventType`, `objectType`, `accountId`, `objectId`, `metaData`, `tenantId`, `userToken`. "By design, events are generic and contain very limited information"; `metaData` is a string or a JSON-serialised metadata object. — [Kill Bill events](https://raw.githubusercontent.com/killbill/killbill-docs/v3/userguide/tutorials/kill_bill_events.adoc)
- Full `ExtBusEventType` enum: ACCOUNT_CREATION, ACCOUNT_CHANGE, BLOCKING_STATE, BROADCAST_SERVICE, SUBSCRIPTION_CREATION, SUBSCRIPTION_PHASE, SUBSCRIPTION_CHANGE, SUBSCRIPTION_UNDO_CHANGE, SUBSCRIPTION_CANCEL, SUBSCRIPTION_UNCANCEL, SUBSCRIPTION_BCD_CHANGE, SUBSCRIPTION_QUANTITY, SUBSCRIPTION_EXPIRED, ENTITLEMENT_CREATION, ENTITLEMENT_CANCEL, BUNDLE_PAUSE, BUNDLE_RESUME, OVERDUE_CHANGE, INVOICE_CREATION, INVOICE_ADJUSTMENT, INVOICE_NOTIFICATION, INVOICE_PAYMENT_SUCCESS, INVOICE_PAYMENT_FAILED, PAYMENT_SUCCESS, PAYMENT_FAILED, TAG_CREATION, TAG_DELETION, CUSTOM_FIELD_CREATION, CUSTOM_FIELD_DELETION, TENANT_CONFIG_CHANGE, TENANT_CONFIG_DELETION. — [ExtBusEventType.java](https://raw.githubusercontent.com/killbill/killbill-plugin-api/master/notification/src/main/java/org/killbill/billing/notification/plugin/api/ExtBusEventType.java)
- `INVOICE_NOTIFICATION` = "An invoice is going to be generated for an account in the future (Can be used to notify customers about upcoming bills)". — [Kill Bill events](https://raw.githubusercontent.com/killbill/killbill-docs/v3/userguide/tutorials/kill_bill_events.adoc)
- Push notifications: register a callback URL per tenant (`/1.0/kb/tenants/registerNotificationCallback?cb=...`); each event is POSTed; on non-2xx, retried per `org.killbill.billing.server.notifications.retries` (example `15m,30m,2h,12h,1d`). Example body: `{"eventType":"TENANT_CONFIG_CHANGE","accountId":null,"objectType":"TENANT_KVS","objectId":"0dfdcc75-...","metaData":"{\"key\":\"PUSH_NOTIFICATION_CB\"}"}` (note `metaData` is a JSON string inside JSON). — [Kill Bill push notifications](https://raw.githubusercontent.com/killbill/killbill-docs/v3/userguide/tutorials/push_notifications.adoc)
- REST calls carry audit headers `X-Killbill-CreatedBy`, `X-Killbill-Reason`, `X-Killbill-Comment` and tenant headers `X-Killbill-ApiKey` / `X-Killbill-ApiSecret`. — [Kill Bill push notifications](https://raw.githubusercontent.com/killbill/killbill-docs/v3/userguide/tutorials/push_notifications.adoc)

Hyperswitch (from source, Apache-2.0):
- Outgoing webhook struct fields: `merchant_id`, `event_id`, `event_type`, `content`, `timestamp`, optional `processor_merchant_id`. — [webhooks.rs](https://raw.githubusercontent.com/juspay/hyperswitch/main/crates/api_models/src/webhooks.rs)
- `EventType` enum variants: PaymentSucceeded, PaymentFailed, PaymentProcessing, PaymentCancelled, PaymentCancelledPostCapture, PaymentAuthorized, PaymentPartiallyAuthorized, PaymentCaptured, PaymentExpired, ActionRequired, RefundSucceeded, RefundFailed, RefundReview, DisputeOpened/Expired/Accepted/Cancelled/Challenged/Won/Lost, MandateActive, MandateRevoked, PayoutSuccess, PayoutFailed, PayoutInitiated, PayoutProcessing, PayoutCancelled, PayoutExpired, PayoutReversed, PayoutNotPermitted, InvoicePaid, SurchargePaymentSucceeded, SurchargeRefundSucceeded. — [enums.rs](https://raw.githubusercontent.com/juspay/hyperswitch/main/crates/common_enums/src/enums.rs)
- It separately models incoming connector webhooks (`IncomingWebhookEvent`: PaymentIntentSuccess, PaymentIntentFailure, RefundSuccess, DisputeOpened, RecoveryPaymentFailure, InvoiceGenerated, ...) and maps them to flows (Payment, Refund, Dispute, Subscription, Mandate, Recovery, ...). — [webhooks.rs](https://raw.githubusercontent.com/juspay/hyperswitch/main/crates/api_models/src/webhooks.rs)

Stripe (practice):
- Each webhook endpoint has an API version that shapes its payloads; "thin event notification payloads are unversioned". Since `2024-09-30.acacia`, monthly releases have no breaking changes and two major releases per year may break. With .NET, Java or Go SDKs "your webhook endpoint's API version must match your SDK's API version so the SDK can deserialize events". — [Stripe webhook versioning](https://docs.stripe.com/webhooks/versioning)
- Documented upgrade procedure is a dual-endpoint migration: create a second endpoint at the new version, receive every event twice, ignore one side (200 for ignored-new, then 400 for ignored-old so they are retried on rollback), then disable the old endpoint. — [Stripe webhook versioning](https://docs.stripe.com/webhooks/versioning)
- Delivery: retries "for up to three days with an exponential back off in live mode"; do not depend on event order; "Track event IDs to identify duplicate deliveries"; in some cases two separate Event objects are generated, so dedup on `data.object` id plus `event.type`; return 2xx quickly before complex logic. — [Stripe webhooks](https://docs.stripe.com/webhooks.md)

Saleor:
- Async webhooks: consumer must answer HTTP 200; "delivery is triggered a maximum of five times" with backoff `10 * (2**retries)` seconds; endpoints must respond within 20 seconds; transports HTTP(S), Google Cloud Pub/Sub, AWS SQS; a queue is recommended because events can be lost when the destination is down. Synchronous webhooks exist for cases where Saleor needs data back (e.g. calculated shipping cost). — [Saleor asynchronous events](https://raw.githubusercontent.com/saleor/saleor-docs/main/docs/developer/extending/webhooks/asynchronous-events.mdx)

OpenMeter:
- Ingests CloudEvents; exposes an OSS REST API with JavaScript, Python and Go SDKs and sends webhooks. — [OpenMeter README](https://raw.githubusercontent.com/openmeterio/openmeter/main/README.md)

### Inferences
- A seed-company Billing service can copy the contract shape without copying code: an envelope of `{event_id, event_type, occurred_at, object_type, <object>}` (Lago/Hyperswitch pattern) plus a unique-key header, at-least-once delivery with a short bounded retry schedule, and a signature header.
- Thin vs fat events is a design lever for the RL environment: fat events (Lago) couple Notifications templates to Billing's object schema, so a field rename breaks consumers; thin events (Kill Bill) force a callback to Billing's REST API and couple consumers to that API instead.
- Lago's storage-dependent dedup (reject-first vs replace-latest) is a real example of the same idempotency key having two different semantics; it is a good model for an "inconsistent duplicate handling across services" task.
- Stripe's note that static-language SDKs must match the endpoint API version maps directly to the seed company's Java (Orders) and C# (Billing) services: strict deserialisers fail on schema drift where Node/Python consumers silently tolerate it.

### Gaps
- Hyperswitch's documented webhook retry schedule and signature header were not read (docs page had moved to `https://docs.hyperswitch.io/integration-guide/webhooks.md`; only source structs were verified).
- Kill Bill's OpenAPI/Swagger spec and its API versioning/deprecation policy were not read; ordering and duplicate guarantees for push notifications are not stated on the pages read.
- Lago's formal API deprecation policy was not found; only the single `event.error` deprecation example and a deprecated field note in the spec.
- OpenMeter's CloudEvents dedup rule (commonly described as `id` + `source`) was **not** verified from a page I opened.
- Medusa, Vendure, Polar, Flexprice and Meteroid event catalogues were not retrieved.
- Standard Webhooks and CloudEvents specs were downloaded but not analysed; no claims are made about them here.

## 4. Notification systems: template/payload coupling, deduplication, breakage on upstream change

### Takeaway
In Novu, a workflow declares a payload schema (JSON Schema or Zod) and step templates read `payload.<field>` directly, so the trigger payload is the contract between the triggering service and the notification service. Deduplication is done with an `Idempotency-Key` header at the API layer, and Novu's docs explicitly say the `transactionId` field does not deduplicate the same way.

### Cited Findings
- Trigger request contents: template (workflow) identifier, list of subscribers (`to`), `payload`, and `overrides`; processing steps are subscriber mapping/validation, workflow validation, attachment upload, queueing; the worker then upserts subscribers from the `to` object, creates one notification entity per subscriber, and creates jobs from workflow steps. — [Novu trigger concepts](https://docs.novu.co/platform/concepts/trigger)
- Job statuses: PENDING, QUEUED, RUNNING, COMPLETED, FAILED, DELAYED (digest/delay), CANCELED; digested events are marked MERGED; in backoff digesting the first event's digest is SKIPPED. — [Novu trigger concepts](https://docs.novu.co/platform/concepts/trigger)
- Payload schema: `payloadSchema` with `type: 'object'`, `properties`, `required: [...]`, and `additionalProperties: false` "to enforce full type strictness, with no rogue properties"; the step body uses fields directly, e.g. ``subject: `You have a new comment from: ${payload.author_name}.` ``. In the docs' own example `author_name` is used in the subject but is not in `required: ['post_id', 'comment']`. — [Novu payload](https://docs.novu.co/framework/payload.md)
- Idempotency: with an `Idempotency-Key` header on `POST /v1/events/trigger`, "only the first is processed"; later duplicates get the cached response; duplicates arriving while the first is in progress get `409 Conflict` and are not queued. The feature "is currently not enabled for all organizations". — [Novu idempotency](https://docs.novu.co/api-reference/idempotency.md)
- `transactionId` "is checked for uniqueness during trigger processing rather than at the API boundary ... useful for tracing and cancellation, but it does not provide the same deduplication or billing protection as an idempotency key". — [Novu idempotency](https://docs.novu.co/api-reference/idempotency.md)
- Digest collapses many events into one notification (the docs note 15 digested events still bill as 15 events). — [Novu trigger concepts](https://docs.novu.co/platform/concepts/trigger)
- Upstream billing systems expose dedicated keys for consumer-side dedup: Lago `X-Lago-Unique-Key`, Hyperswitch `event_id`, Stripe event `id`. — [Lago webhook format](https://getlago.com/docs/api-reference/webhooks/format---signature.md), [webhooks.rs](https://raw.githubusercontent.com/juspay/hyperswitch/main/crates/api_models/src/webhooks.rs), [Stripe webhooks](https://docs.stripe.com/webhooks.md)
- Kill Bill provides a pre-notification event (`INVOICE_NOTIFICATION`) specifically so a notifier can warn about an upcoming bill, and its generic events contain only ids, so a notification plugin must look up the object to fill a template. — [Kill Bill events](https://raw.githubusercontent.com/killbill/killbill-docs/v3/userguide/tutorials/kill_bill_events.adoc)
- Online Boutique and the OpenTelemetry demo both include an email service called by checkout to send an order confirmation (Online Boutique: `emailservice`, Python, "Sends users an order confirmation email (mock)"; OTel demo: checkout → email over HTTP, email in Ruby). — [Online Boutique README](https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/main/README.md), [OTel demo architecture](https://raw.githubusercontent.com/open-telemetry/opentelemetry.io/main/content/en/docs/demo/architecture.md)

### Inferences
- What breaks when an upstream payload changes (derived from the schema mechanics above, not from a documented incident):
  - Renaming or removing a field that a template reads: with a strict schema (`required` + `additionalProperties: false`) the trigger is rejected at validation; with a loose schema the template renders an empty or "undefined" value and the message is sent wrong. Novu's own example (optional `author_name` used in the subject) shows the silent variant.
  - Adding a new field upstream: harmless under loose schemas, but rejected under `additionalProperties: false`, so a purely additive upstream change can still break a strict consumer.
  - Changing type or unit (cents to decimal, enum value rename, date format): passes schema checks that only check type, renders a wrong amount or picks the wrong template branch.
  - Changing the dedup key source (e.g. Billing starts retrying with a new event id per attempt): customers receive duplicate emails.
- For a few-hundred-line Python Notifications service, the imitable core is: a template registry keyed by event type, a per-template declared payload schema, a rendered-message log keyed by `(event_id, channel, recipient)` for dedup, and an explicit policy for missing variables (fail vs default).

### Gaps
- No Novu page read states what is rendered when a template variable is missing from the payload, or whether schema validation failure returns 4xx at trigger time versus failing the job; the breakage list above is inference.
- listmonk, Apprise and Notifo template/dedup behaviour was not examined; only their licence and metadata are verified.
- No published incident report of a notification outage caused by an upstream payload change was found (search was unavailable).

## 5. Research benchmarks: service graphs, fault types, fault-injection studies, and which faults are cross-service coordination faults

### Takeaway
Train Ticket's 22 replicated industrial fault cases are the richest documented source of cross-service coordination faults: by my reading about 9 of the 22 involve an interaction between services (ordering, missing propagated data, unexpected upstream output, shared-library version skew), while most newer RCA datasets (RCAEval RE1/RE2, OTel demo flags) inject resource, network or single-service faults. DeathStarBench documents service graphs and workloads but its repository documents no fault catalogue.

### Cited Findings

Train Ticket (Zhou et al., "Fault Analysis and Debugging of Microservice Systems", replication package):
- System: "41 microservices", 4 languages (Java, Node.js, Python, Go), Docker Swarm or Kubernetes; functions are ticket enquiry, reservation, payment, change and user notification. — [Replication package site](https://fudanselab.github.io/research/MSFaultEmpiricalStudy/)
- The fault-replication repo has 22 branches, one per industrial fault case (F1–F22), each with an "industrial fault description" and a "TrainTicket replicated fault description". — [train-ticket-fault-replicate README](https://raw.githubusercontent.com/FudanSELab/train-ticket-fault-replicate/master/README.md)
- Root causes as tabulated on the site: F1 "Asynchronous message delivery lacks sequence control"; F2 "Different data requests for the same report are returned in an unexpected order"; F3 "JVM configurations are inconsistent with Docker configurations"; F4 SSL offloading at too fine a granularity; F5 "The high load of a type of requests causes the timeout failure of another type of requests"; F6 "Endless recursive requests of a microservice are caused by SQL errors of another dependent microservice"; F7 "The overload of requests to a third-party service leads to denial of service"; F8 "The key in the request of one microservice is not passed to its dependent microservice"; F9 CSS RTL display error; F10 "An API used in a special case of BOM updating returns unexpected output"; F11 "The BOM data is updated in an unexpected sequence"; F12 "Price status querying does not consider an unexpected output of a microservice in its call chain"; F13 "Price optimization steps are executed in an unexpected order"; F14 mistake in CPI calculation; F15 wrong Spark actor configuration; F16 `max-content-length` too small for upload; F17 too many nested SQL selects; F18 "One key of the returned JSON data for the UI chart includes the null value"; F19 price not formatted correctly in French format; F20 JBoss classpath lacks the right DB2 jar; F21 missing aria label; F22 wrong column name in constructed SQL. — [Replication package site](https://fudanselab.github.io/research/MSFaultEmpiricalStudy/)
- Replications that are explicitly cross-service:
  - F1: cancel flow where Cancel service calls Inside-Payment to "drawback money" and Order service to reset status; a random delay makes "[Reset Order Status] ... complete before [Drawback Money]".
  - F8: "the VIP user has one more key/token to be used in ticket-booking process ... the key/token is missing when delivering" between services.
  - F10: "In contacts service we have two APIs serve for the ticket reservation process in different situation ... these APIs may be wrongly invoked".
  - F11: "two microservices set the same value in the database in order cancellation process" in the wrong sequence, with a non-deterministic recheck.
  - F12: fault occurs only in a specific state of Order service (locked station list), so cancel requests from another service are rejected.
  - F13: "confirming cancellation is already begun but the payment process is still not completed yet".
  - F18: `getFood` returns null and "the front stage should get the first item ... without check whether it's null".
  - F19: returned price displayed in the wrong locale format.
  - F20 (as replicated): "Many microservices share a same lib. This lib contains ... Enum of Order status. The value of same order status in different version is in different value. If some microservice use an old version lib but some use a new version lib, the fault will occur."
  — [train-ticket-fault-replicate README](https://raw.githubusercontent.com/FudanSELab/train-ticket-fault-replicate/master/README.md)
- Other interaction-style faults: F5 (thread-pool exhaustion in Basic-Info-Service when two callers compete), F6 (caller retries forever on a dependent service's SQL error until timeout), F7 (third-party Node.js payment service delay triggers timeout), F3 (JVM memory limit larger than Docker limit), F15 as replicated (nginx body-size limit of 200 bytes blocks larger request bodies). — [train-ticket-fault-replicate README](https://raw.githubusercontent.com/FudanSELab/train-ticket-fault-replicate/master/README.md)
- The debugging study compared basic logs, visual logs and visual traces per fault; for F3 and F4 the site's table marks the attempts as "Failed". — [Replication package site](https://fudanselab.github.io/research/MSFaultEmpiricalStudy/)

DeathStarBench (Gan et al., ASPLOS 2019):
- "five end-to-end services, four for cloud systems, and one for cloud-edge systems running on drone swarms"; released: Social Network, Media Service, Hotel Reservation; "in progress": E-commerce site, Banking System, Drone coordination. — [DSB README](https://raw.githubusercontent.com/delimitrou/DeathStarBench/master/README.md)
- Social Network: "unidirectional follow relationships, implemented with loosely-coupled microservices, communicating with each other via Thrift RPCs"; actions include create post, read timelines, recommendations, search, register/login, follow/unfollow; Nginx frontend on 8080, Jaeger on 16686. — [DSB socialNetwork README](https://raw.githubusercontent.com/delimitrou/DeathStarBench/master/socialNetwork/README.md)
- Hotel Reservation: Go and gRPC, derived from `harlow/go-micro-services`, extended with in-memory and persistent databases, a recommender and reservation placement. — [DSB hotelReservation README](https://raw.githubusercontent.com/delimitrou/DeathStarBench/master/hotelReservation/README.md)

RCAEval (WWW 2025 / ASE 2024):
- "nine datasets with 735 real failure cases" across Online Boutique, Sock Shop and Train Ticket, 11 fault types. RE1 (375 cases, metrics only): cpu, mem, disk, delay, loss. RE2 (270 cases, metrics+logs+traces): adds socket. RE3 (90 cases): "code-level faults (F1-F5)". — [RCAEval README](https://raw.githubusercontent.com/phamquiluan/RCAEval/main/README.md)
- Code-level example: "Incorrect parameter values" injected in Online Boutique `cartservice` (`AddItemAsync` called with an extremely large quantity), causing failures "in all its callers"; root-cause indicator is a stack trace in logs. — [RCAEval code-level notebook](https://raw.githubusercontent.com/phamquiluan/RCAEval/main/docs/code-level-rca.ipynb)
- As of 2026 it also ships an agent evaluation path (`rcaeval-agent export/evaluate`, blind task view with anonymised case ids, MCP server). — [RCAEval README](https://raw.githubusercontent.com/phamquiluan/RCAEval/main/README.md)

OpenTelemetry Demo:
- Service graph (documented as a Mermaid diagram): frontend-proxy (Envoy) → frontend (TypeScript) → ad (Java), cart (.NET, Valkey cache), currency (C++), checkout (Go), shipping (Rust) → quote (PHP), product-catalog (Go, PostgreSQL), recommendation (Python); checkout → payment (JavaScript), email (Ruby), Kafka queue → accounting (.NET) and fraud-detection (Kotlin); flagd for feature flags. — [OTel demo architecture](https://raw.githubusercontent.com/open-telemetry/opentelemetry.io/main/content/en/docs/demo/architecture.md)
- Fault flags include `adFailure`, `adHighCpu`, `cartFailure`, `emailMemoryLeak`, `failedReadinessProbe`, `imageSlowLoad`, `intlShippingSlowdown`, `kafkaConsumerDead`, `kafkaQueueProblems`, `paymentFailure`, `paymentUnreachable` ("Use a bad address when calling the Payment service"), `productCatalogFailure` (errors for product id `OLJCESPC7Z`), `productCatalogLockContention`, `recommendationCacheFailure`. — [OTel demo feature flags](https://raw.githubusercontent.com/open-telemetry/opentelemetry.io/main/content/en/docs/demo/feature-flags/_index.md)

Other suites and datasets:
- Online Boutique: 11 services in Go, C#, Node.js, Python, Java; `checkoutservice` "Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification". — [Online Boutique README](https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/main/README.md)
- TeaStore: "five distinct services plus a registry" (WebUI, Auth, Recommender, Persistence, Image Provider), REST with Netflix Ribbon client-side load balancing, Kieker-instrumented variants; published at MASCOTS 2018. — [TeaStore README](https://raw.githubusercontent.com/DescartesResearch/TeaStore/master/README.md), [TeaStore GET_STARTED](https://raw.githubusercontent.com/DescartesResearch/TeaStore/master/GET_STARTED.md)
- µBench: generates "dummy" microservice applications with a configurable dependency graph, stress functions (CPU, memory, I/O, network), HTTP or gRPC; the quick start is a 10-service star topology; paper in IEEE TPDS 34(3), 2023. — [µBench README](https://raw.githubusercontent.com/mSvcBench/muBench/main/README.md)
- Alibaba microservices trace v2021: "nearly twenty thousand microservices", over ten thousand bare-metal nodes, twelve hours; tables for node, MS resource, MS metrics (call rate, response time) and call graphs sampled at 0.5% (more than twenty million call graphs); three communication paradigms (inter-process communication, remote invocation, indirect communication); analysed in Luo et al., SoCC'21. v2022 extends to 13 days and adds service id in the call graph. — [v2021 README](https://raw.githubusercontent.com/alibaba/clusterdata/master/cluster-trace-microservices-v2021/README.md), [v2022 README](https://raw.githubusercontent.com/alibaba/clusterdata/master/cluster-trace-microservices-v2022/README.md)
- Online Marketplace benchmark targets "core data management challenges that existing benchmarks fail to address", listing "transaction processing, query processing, event processing, constraint enforcement, and data replication". — [arXiv:2403.12605](http://arxiv.org/abs/2403.12605v4)
- A 2025 study reports that "simple rule-based methods can achieve performance comparable to or even surpassing state-of-the-art (SOTA) models on four widely used public benchmarks", attributing this to oversimplified fault injection. — [arXiv:2510.04711](http://arxiv.org/abs/2510.04711v2)
- A 2026 audit of OpenRCA, RCAEval and PetShop ran 16 methods on 11 subsystems and found pooled leaderboard leads often do not hold per subsystem. — [arXiv:2606.29159](http://arxiv.org/abs/2606.29159v2)

### Inferences
- My classification of the 22 Train Ticket cases (not the paper's own taxonomy):
  - Missing coordination / ordering across services: F1, F2, F11, F13 (and F12 as a state-dependent variant).
  - Interface or data-contract mismatch: F8 (field not propagated), F10 (wrong API variant for a case), F18 (null in returned JSON unhandled by consumer), F19 (format/locale of a price), F20 as replicated (shared enum values differ across library versions).
  - Cross-service resilience: F5 (shared resource exhaustion), F6 (retry storm on dependency error), F7 (third-party timeout).
  - Configuration inconsistency between layers: F3, F4, F15/F16 (size limits).
  - Single-service logic or UI defects: F9, F14, F17, F21, F22.
- F20's replication (order-status enum numbering differs between library versions) and F1/F13 (cancel versus refund/payment ordering) translate almost directly to a subscription retailer: Orders and Billing disagreeing on status enum values, or a cancel racing a charge.
- Resource/network fault datasets (RCAEval RE1/RE2, most OTel flags) test diagnosis, not coordination; the coordination-fault material is concentrated in Train Ticket's industrial cases and, for data consistency, the Online Marketplace benchmark.
- Service-graph shape for a four-service seed company is best matched by the checkout fan-out in Online Boutique / OTel demo (checkout → payment → email, plus an async queue to accounting), not by Train Ticket's 41-service graph.

### Gaps
- The Train Ticket TSE paper itself (survey size, fault category percentages) and the DeathStarBench ASPLOS paper (service counts per application, dependency-graph statistics) were not opened; only repositories and the replication site were read, so no numbers from the papers are reported.
- RCAEval's precise definitions of code-level faults f1–f5 were not found in the README; only one example ("Incorrect parameter values") is verified.
- AIOpsLab, ITBench, SREGym, OpenRCA and Aegis fault catalogues were not read; only their existence and licence line were confirmed.
- No DeathStarBench fault-injection study was verified.
- No public dataset of Alibaba-scale interface-mismatch or schema-drift incidents was found.

## 6. Parts small and clear enough to imitate in a few hundred lines

### Takeaway
The most reusable small pieces are contract shapes and rule tables rather than code: Lago's webhook envelope with unique-key header, Kill Bill's typed invoice-item list and overdue state machine, the Lago upgrade/downgrade and proration rule with its worked example, Novu's payload-schema-per-workflow, and Stripe-style idempotency-key semantics.

### Cited Findings
- Webhook envelope plus three headers (unique key, signature, algorithm) and "3 attempts, waiting longer between each" fit on one page. — [Lago webhook format](https://getlago.com/docs/api-reference/webhooks/format---signature.md)
- Kill Bill's thin event is five to seven fields with a fixed enum of 31 event types. — [Kill Bill events](https://raw.githubusercontent.com/killbill/killbill-docs/v3/userguide/tutorials/kill_bill_events.adoc), [ExtBusEventType.java](https://raw.githubusercontent.com/killbill/killbill-plugin-api/master/notification/src/main/java/org/killbill/billing/notification/plugin/api/ExtBusEventType.java)
- Invoice-item taxonomy and credit balance mechanism (RECURRING/FIXED/USAGE/TAX, REPAIR_ADJ, ITEM_ADJ, CREDIT_ADJ, CBA_ADJ) and the overdue conditions/actions list. — [Kill Bill subscription guide](https://docs.killbill.io/latest/userguide_subscription)
- Upgrade/downgrade decision rule (compare yearly amounts; upgrade immediate, downgrade at period end) with a testable numeric example (€45.16 and €109.68). — [Lago upgrades and downgrades](https://getlago.com/docs/guide/subscriptions/upgrades-downgrades.md)
- Usage-event dedup table (two backends, two behaviours). — [Lago ingesting usage](https://getlago.com/docs/guide/events/ingesting-usage.md)
- Dunning campaign as three parameters (threshold per currency, delay in days, attempts). — [Lago automatic dunning](https://getlago.com/docs/guide/dunning/automatic-dunning.md)
- Idempotency-key rules (store first response including 500s, compare parameters, 24-hour retention, do not store on validation failure) and Novu's `409 Conflict` for in-flight duplicates. — [Stripe idempotent requests](https://docs.stripe.com/api/idempotent_requests), [Novu idempotency](https://docs.novu.co/api-reference/idempotency.md)
- Payload schema per workflow (JSON Schema with `required` and `additionalProperties`). — [Novu payload](https://docs.novu.co/framework/payload.md)
- Small polyglot service graphs with an orchestrating checkout and a mock email service: Online Boutique (11 services) and TeaStore (5 services + registry). — [Online Boutique README](https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/main/README.md), [TeaStore README](https://raw.githubusercontent.com/DescartesResearch/TeaStore/master/README.md)
- Fault toggles behind feature flags, one line per fault with the affected service named. — [OTel demo feature flags](https://raw.githubusercontent.com/open-telemetry/opentelemetry.io/main/content/en/docs/demo/feature-flags/_index.md)
- Each Train Ticket fault is a branch with a two-paragraph description (industrial case, then replication), a format that can be reused for seed-company task cards. — [train-ticket-fault-replicate README](https://raw.githubusercontent.com/FudanSELab/train-ticket-fault-replicate/master/README.md)

### Inferences
- Suggested imitation targets per seed service (my recommendation):
  - Billing (C#): subscription state machine using Lago's five statuses; invoice with integer-cent totals and Kill Bill-style typed items; day-count proration; credit vs refund vs offset; a three-parameter dunning loop; `Idempotency-Key` on POST; outbound events with envelope + unique key. The permissive C# reference for service layout is `dotnet/eShop` (MIT).
  - Notifications (Python): template registry keyed by event type with declared payload schema; dedup log; optional digest. Notifo (MIT, C#) and Apprise (BSD-2, Python) are the permissive references; Novu core is MIT but its `enterprise/` tree is proprietary.
  - Orders (Java) and Storefront (TypeScript): consumer side of the same contracts; strict deserialisation in Java makes schema drift visible, which is useful for coordination tasks.
- Coordination-fault seeds that map cleanly from documented cases: enum value skew (Train Ticket F20), missing propagated field (F8), null field unhandled by consumer (F18), price/locale formatting (F19), cancel-versus-refund ordering (F1/F13), retry storm on dependency error (F6), duplicate-handling mismatch (Lago's two dedup modes), additive field rejected by strict schema (Novu `additionalProperties: false`), webhook payload version skew (Stripe versioned endpoints).

### Gaps
- No code was read or measured for line counts in any repository; "few hundred lines" judgements refer to the size of the documented contract or rule, not to the size of the upstream implementation.
- I did not verify whether `dotnet/eShop` includes a payment/billing-style service or webhook contracts beyond its README.
