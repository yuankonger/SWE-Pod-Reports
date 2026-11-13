# Public multi-service, multi-language "storefront" reference applications (state as of 2026-11-11)

Method note for the report writer (applies to every section):

- Repo metadata (licence SPDX id, stars, `pushed_at`, archived flag) was read from the GitHub REST API (`api.github.com/repos/<owner>/<repo>`) on 2026-11-11. `pushed_at` covers pushes to *any* branch (including bot branches), so it can be much later than the last commit on the default branch.
- "HEAD date" is the committer date of the default-branch HEAD from a shallow clone taken on 2026-11-11.
- Release dates are the commit dates of the release tags (fetched with git), cross-checked against the GitHub releases pages where stated.
- Lines of code are my own count: raw line counts (blank lines and comments included) of source files by extension, per service directory, excluding generated/vendored paths (`genproto`, `*_pb2*`, `*.pb.go`, `Migrations`, `static`, `assets`, `dist`, `vendor`). They are approximate and are not a `cloc` figure. "Test-ish lines" means lines in files whose path contains `test` or `spec`.
- Nothing was built or run. Build/run weight is taken from each project's own docs.
- No code was copied; only directory listings, READMEs and contract file names were read.

## 1. Inventory: repository, licence, stars, activity, service count, languages, size

### Takeaway
Of the four required systems, Online Boutique, the OpenTelemetry Demo and dotnet/eShop are actively maintained (commits in Oct to Nov 2026); eShopOnContainers and the whole Sock Shop organisation are read-only archives since late 2023. Services in the polyglot demos are small: typically 200 to 1,000 source lines each, with frontends the only parts above about 2,000 lines.

### Cited Findings

#### Summary table (GitHub API, 2026-11-11)

| System | Repo | Licence (SPDX per GitHub) | Stars | Default-branch HEAD | `pushed_at` | Latest release tag | Status |
|---|---|---|---|---|---|---|---|
| Online Boutique | GoogleCloudPlatform/microservices-demo | Apache-2.0 | 21,179 | 2026-10-27 | 2026-10-27 | v0.10.7 (2026-09-18) | Active |
| OpenTelemetry Demo (Astronomy Shop) | open-telemetry/opentelemetry-demo | Apache-2.0 | 3,449 | 2026-11-10 | 2026-11-10 | 3.1.0 (2026-09-18) | Active |
| eShop | dotnet/eShop | MIT | 11,017 | 2026-10-15 | 2026-11-09 | no version releases found (only a `dotnet8` tag) | Active |
| eShopOnContainers | dotnet-architecture/eShopOnContainers | GitHub reports none; `dev` branch LICENSE is MIT | 24,283 | 2023-11-15 | 2023-11-15 | not checked | Archived |
| Sock Shop | microservices-demo/microservices-demo | Apache-2.0 | 3,779 | 2023-12-05 | 2023-12-05 | 0.0.12 (2016-08-02) | Archived |
| AWS Retail Store Sample | aws-containers/retail-store-sample-app | MIT-0 | 616 | 2026-09-25 | 2026-11-11 | v1.6.3 (2026-09-25) | Active |
| Spring PetClinic Microservices | spring-petclinic/spring-petclinic-microservices | Apache-2.0 | 2,240 | 2026-10-23 | 2026-10-23 | v3.4.1 (2024-12-28) | Active |
| FTGO | microservices-patterns/ftgo-application | GitHub: NOASSERTION; `LICENSE.md` is Apache-2.0 text, "Copyright 2016 Eventuate, Inc." | 3,785 | 2022-09-03 | 2026-03-13 | not checked | Not archived; default branch stale |
| flowing-retail | berndruecker/flowing-retail | Apache-2.0 | 1,332 | 2023-11-21 | 2024-08-01 | not checked | Not archived; stale |
| Stan's Robot Shop | instana/robot-shop | Apache-2.0 | 1,015 | 2023-03-06 | 2026-05-14 | no tags | Archived |
| TeaStore | DescartesResearch/TeaStore | Apache-2.0 | 167 | 2025-01-08 | 2025-01-08 | v1.4.2 (2022-08-16) | Not archived; low activity |
| AKS Store Demo | Azure-Samples/aks-store-demo | MIT | 316 | 2026-11-03 | 2026-11-12 | 2.2.0 (2026-06-22) | Active |
| Bank of Anthos (banking, not retail) | GoogleCloudPlatform/bank-of-anthos | Apache-2.0 | 1,475 | 2026-09-18 | 2026-11-03 | v0.6.11 (2026-09-18) | Active |
| MuShop | oracle-quickstart/oci-cloudnative | UPL-1.0 | 275 | 2025-06-13 | 2026-11-11 | not checked | Not archived; default branch quiet |
| Pitstop (garage, not retail) | EdwinVW/pitstop | Apache-2.0 | 1,166 | 2026-10-29 | 2026-10-29 | not checked | Active |
| YAS | nashtech-garage/yas | MIT | 1,992 | 2026-06-12 | 2026-06-12 | not checked | Active earlier in 2026 |
| Train Ticket | FudanSELab/train-ticket | Apache-2.0 | 927 | 2022-11-01 | 2025-11-21 | not checked | Not archived; default branch stale |
| Dapr quickstarts | dapr/quickstarts | Apache-2.0 | 1,117 | not cloned | 2026-11-09 | not checked | Active |

Sources: [Online Boutique](https://github.com/GoogleCloudPlatform/microservices-demo), [OTel Demo](https://github.com/open-telemetry/opentelemetry-demo), [eShop](https://github.com/dotnet/eShop), [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers), [Sock Shop](https://github.com/microservices-demo/microservices-demo), [Retail Store](https://github.com/aws-containers/retail-store-sample-app), [PetClinic MS](https://github.com/spring-petclinic/spring-petclinic-microservices), [FTGO](https://github.com/microservices-patterns/ftgo-application), [flowing-retail](https://github.com/berndruecker/flowing-retail), [Robot Shop](https://github.com/instana/robot-shop), [TeaStore](https://github.com/DescartesResearch/TeaStore), [AKS Store Demo](https://github.com/Azure-Samples/aks-store-demo), [Bank of Anthos](https://github.com/GoogleCloudPlatform/bank-of-anthos), [MuShop](https://github.com/oracle-quickstart/oci-cloudnative), [Pitstop](https://github.com/EdwinVW/pitstop), [YAS](https://github.com/nashtech-garage/yas), [Train Ticket](https://github.com/FudanSELab/train-ticket), [Dapr quickstarts](https://github.com/dapr/quickstarts).

Other repos for which only API metadata was collected (not opened further):

- thangchung/go-coffeeshop: MIT, 4,361 stars, last push 2023-05-10 — [Source](https://github.com/thangchung/go-coffeeshop)
- vietnam-devs/coolstore-microservices: MIT, 2,533 stars, last push 2023-03-07 — [Source](https://github.com/vietnam-devs/coolstore-microservices)
- mehdihadeli/food-delivery-microservices: MIT, 1,017 stars, last push 2026-10-14 — [Source](https://github.com/mehdihadeli/food-delivery-microservices)
- eventuate-tram/eventuate-tram-examples-customers-and-orders: GitHub licence NOASSERTION, 722 stars, last push 2026-10-22 — [Source](https://github.com/eventuate-tram/eventuate-tram-examples-customers-and-orders)
- cer/event-sourcing-examples: NOASSERTION, 3,156 stars, last push 2020-12-23 — [Source](https://github.com/cer/event-sourcing-examples)
- delimitrou/DeathStarBench: Apache-2.0, 965 stars, last push 2024-07-09 — [Source](https://github.com/delimitrou/DeathStarBench)
- dotnet/eShopSupport: MIT, 664 stars, last push 2025-05-16 — [Source](https://github.com/dotnet/eShopSupport)
- Azure-Samples/eShopOnAzure: MIT, 280 stars, archived, last push 2024-09-09 — [Source](https://github.com/Azure-Samples/eShopOnAzure)
- asc-lab/micronaut-microservices-poc: Apache-2.0, 498 stars, last push 2022-08-13 — [Source](https://github.com/asc-lab/micronaut-microservices-poc)
- acmeair/acmeair: Apache-2.0, 144 stars, last push 2024-03-09 — [Source](https://github.com/acmeair/acmeair)
- kgrzybek/modular-monolith-with-ddd: MIT, 14,132 stars, last push 2024-06-04 (a monolith, listed only as a size reference) — [Source](https://github.com/kgrzybek/modular-monolith-with-ddd)

#### Online Boutique (GoogleCloudPlatform/microservices-demo)

- The README service table lists 11 entries: frontend (Go), cartservice (C#), productcatalogservice (Go), currencyservice (Node.js), paymentservice (Node.js), shippingservice (Go), emailservice (Python), checkoutservice (Go), recommendationservice (Python), adservice (Java), loadgenerator (Python/Locust) — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/README.md)
- The `src/` directory has 12 subdirectories; the twelfth is `shoppingassistantservice` (one Python file, 120 lines), which the README table does not list — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/src)
- Approximate source size per service (my count, generated protobuf code excluded): adservice Java 354 lines / 2 files; cartservice C# 868 / 9; checkoutservice Go 771 / 3; currencyservice JS 266 / 2; emailservice Python 280 / 3; frontend Go 1,896 / 10; loadgenerator Python 92 / 1; paymentservice JS 294 / 4; productcatalogservice Go 562 / 4; recommendationservice Python 236 / 3; shippingservice Go 484 / 4 — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/src)
- Latest release v0.10.7 is marked "Latest" on the releases page, preceded by v0.10.6 and v0.10.5 — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/releases)
- Academic papers disagree on the count: papers found describe it as having 11 services or 12 services — [RCAEval](https://arxiv.org/pdf/2412.17015); [search summary also drew on](https://arxiv.org/pdf/2405.09330)

#### OpenTelemetry Demo (open-telemetry/opentelemetry-demo)

- The official architecture page lists these services and languages: Accounting (.NET), Ad (Java), Agent (Python), Cart (.NET), Chatbot (Python), Checkout (Go), Currency (C++), Email (Ruby), Flagd (Go), Flagd-ui (Elixir), Fraud Detection (Kotlin), Frontend (TypeScript), Frontend Proxy (Envoy, C++), Image Provider (nginx, C++), Load Generator (Locust, Python), MCP (Python), Payment (JavaScript), Product Catalog (Go), Quote (PHP), Recommendation (Python), Shipping (Rust), React Native App (TypeScript), plus Kafka, Valkey and PostgreSQL — [Source](https://opentelemetry.io/docs/demo/architecture/)
- Conflict: the repo's `main` branch at HEAD (2026-11-10) has the Recommendation service as Java (Gradle build; README says it uses the OpenTelemetry Spring Boot starter), and an unreleased changelog entry reads "Rewrite the recommendation service in Java with Spring Boot 4" (issue 1368) — [Source](https://github.com/open-telemetry/opentelemetry-demo/tree/main/src/recommendation); contradicted by [docs page still listing Python](https://opentelemetry.io/docs/demo/architecture/). The docs describe release 3.1.0; `main` is ahead.
- `src/` has 32 subdirectories, but 11 of them contain no application source in the languages counted (flagd, frontend-proxy, grafana, image-provider, jaeger, kafka, opamp-server, opensearch, otel-collector, postgresql, prometheus, telemetry-docs are configuration or third-party images) — [Source](https://github.com/open-telemetry/opentelemetry-demo/tree/main/src)
- Approximate source size per service at HEAD (my count): accounting C# 333 lines / 5 files; ad Java 624 / 4; agent Python 536 / 6; cart C# 963 / 8; chatbot Python 456 / 3; checkout Go 1,398 / 6; currency C++ 572 / 4; email Ruby 102 / 1; flagd-ui Elixir 3,565 / 37; fraud-detection Kotlin 133 / 1; frontend TypeScript 9,157 / 108; load-generator Python 315 / 1; mcp Python 82 / 2; payment JS 203 / 3; product-catalog Go 802 / 4; quote PHP 284 / 6; react-native-app TypeScript 5,663 / 33; recommendation Java 555 / 5; shipping Rust 632 / 7 — [Source](https://github.com/open-telemetry/opentelemetry-demo/tree/main/src)
- Latest release 3.1.0 is marked "Latest"; the releases page warns users of 3.0.0 to use 3.1.0 instead; 2.2.0 precedes them — [Source](https://github.com/open-telemetry/opentelemetry-demo/releases)
- The repo ships `AGENTS.md` and `CLAUDE.md` files with rules for AI-assisted contributions (for example, agents must not post generated text on issues or PRs) — [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/AGENTS.md)

#### dotnet/eShop

- README describes it as "A reference .NET application implementing an e-commerce website using a services-based architecture with Aspire" — [Source](https://github.com/dotnet/eShop/blob/main/README.md)
- `src/` has 20 projects, all C#/Razor: Basket.API, Catalog.API, Identity.API, Ordering.API, OrderProcessor, PaymentProcessor, Webhooks.API, WebhookClient, WebApp, WebAppComponents, ClientApp, HybridApp, plus libraries EventBus, EventBusRabbitMQ, IntegrationEventLogEF, Ordering.Domain, Ordering.Infrastructure, Shared, eShop.ServiceDefaults and the eShop.AppHost orchestrator — [Source](https://github.com/dotnet/eShop/tree/main/src)
- Approximate size (my count, migrations excluded): Basket.API 300 lines / 11 files; Catalog.API 1,206 / 33; Identity.API 2,592 / 60; Ordering.API 2,047 / 68 (plus Ordering.Domain 700 / 23 and Ordering.Infrastructure 445 / 14); OrderProcessor 176 / 7; PaymentProcessor 72 / 7; Webhooks.API 455 / 24; WebApp about 3,200 across Razor, JS and C#; ClientApp (MAUI) 7,230 / 137 — [Source](https://github.com/dotnet/eShop/tree/main/src)
- README links a separate `release/8.0` branch for .NET 8; `main` requires the .NET 10 SDK (`global.json` pins 10.0.302) — [Source](https://github.com/dotnet/eShop/blob/main/README.md)

#### eShopOnContainers (predecessor)

- The default branch `repo_moved` contains only a README: "As of November 2023, the eShop sample application has been updated and moved to https://github.com/dotnet/eShop... This repo is now a read-only archive... the old code... in the 'dev' branch" — [Source](https://github.com/dotnet-architecture/eShopOnContainers)
- The `dev` branch LICENSE begins "MIT License / Copyright (c) .NET Foundation and Contributors"; GitHub's API reports no licence because the default branch has no LICENSE file — [Source](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/LICENSE)
- The `dev` README lists Basket API, Catalog API, Identity API, Ordering API, Ordering SignalR hub, Payment API, Webhooks, Web and Mobile Shopping Aggregators, and Web MVC, Web SPA and Web Status client apps — [Source](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev)

#### Sock Shop (microservices-demo organisation)

- All 23 repositories in the organisation are public archives, last updated 2023-12-05; the organisation was marked archived on 2023-12-29 — [Source](https://github.com/orgs/microservices-demo/repositories?type=all)
- Service code lives in separate repos, one per service: front-end (GitHub language label HTML), user (Go), catalogue (Go), payment (Go), carts (Java), orders (Java), shipping (Java), queue-master (Java); alternates orders.NET (C#) and orders-aws (Scala) also exist. All are Apache 2.0 except e2e-tests, deploy_doc and travis-cron_tools (MIT) — [Source](https://github.com/orgs/microservices-demo/repositories?type=all)
- The main repo holds deployment files, docs and an `openapi` test harness, not service code — [Source](https://github.com/microservices-demo/microservices-demo)
- The design doc says the architecture "was intentionally designed to provide as many microservices as possible" and is "intentionally polyglot" — [Source](https://github.com/microservices-demo/microservices-demo/blob/master/internal-docs/design.md)
- Papers disagree on its size, with counts from 6 to 15 services reported — [RCAEval](https://arxiv.org/pdf/2412.17015); [FastFI](https://arxiv.org/pdf/2601.14800)

#### AWS Retail Store Sample App

- README component table: UI (Java), Catalog (Go), Cart (Java), Orders (Java), Checkout (Node) — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/README.md)
- Approximate size (my count): ui Java 11,438 lines / 125 files; cart Java 1,892 / 27; catalog Go 1,788 / 14; orders Java 2,563 / 42; checkout TypeScript 2,765 / 42 — [Source](https://github.com/aws-containers/retail-store-sample-app/tree/main/src)
- `src/recommendations` exists but contains only `openapi.yml` and `README.md` (a specification without an implementation) — [Source](https://github.com/aws-containers/retail-store-sample-app/tree/main/src/recommendations)
- The LICENSE is the MIT No Attribution text ("Copyright Amazon.com, Inc. or its affiliates") — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/LICENSE)

#### Others

- Spring PetClinic Microservices: 8 Maven modules, all Java: api-gateway (824 lines), customers-service (939), vets-service (389), visits-service (359), genai-service (628), config-server (60), discovery-server (60), admin-server (31) — [Source](https://github.com/spring-petclinic/spring-petclinic-microservices)
- FTGO: Java throughout apart from a JS GraphQL gateway. Services: order (4,262 lines / 94 files), kitchen (1,102), delivery (1,211), accounting (678), consumer (574), restaurant (580), order-history (1,495), api-gateway (606), api-gateway-graphql (JS, 533) — [Source](https://github.com/microservices-patterns/ftgo-application)
- flowing-retail: Java only; three variants (`kafka`, `rest`, `zeebe`). The Kafka variant has checkout (350 lines), order-zeebe (884), payment (257), inventory (383), shipping (311), monitor (348) — [Source](https://github.com/berndruecker/flowing-retail/tree/master/kafka/java)
- Robot Shop: README lists NodeJS (Express), Java (Spring Boot), Python (Flask), Golang, PHP (Apache), MongoDB, Redis, MySQL, RabbitMQ, Nginx, AngularJS. Sizes: cart JS 407 lines in 1 file; catalogue JS 188 / 1; user JS 303 / 1; payment Python 207 / 2; shipping Java 600 / 11; ratings PHP 599 / 11; dispatch Go 233 / 1 — [Source](https://github.com/instana/robot-shop)
- TeaStore: "five distinct services plus a registry", all Java: auth (766 lines), image (6,677), persistence (4,182), recommender (3,078), webui (Java 1,902 plus JS), registry (426) — [Source](https://github.com/DescartesResearch/TeaStore)
- AKS Store Demo: makeline-service (Go, 1,022 lines), order-service (JavaScript, 415), product-service (Rust, 1,109), store-front and store-admin (Vue.js/TypeScript), virtual-customer and virtual-worker (Rust), ai-service (Python, 446, optional) — [Source](https://github.com/Azure-Samples/aks-store-demo/blob/main/README.md)
- Bank of Anthos: frontend (Python, 882 lines), user-service (Python, 837), contacts (Python, 853), ledger-writer (Java, 1,364), balance-reader (Java, 1,006), transaction-history (Java, 1,027), loadgenerator (Python/Locust), two PostgreSQL databases — [Source](https://github.com/GoogleCloudPlatform/bank-of-anthos/blob/main/README.md)
- MuShop: api (JS, 2,514 lines), carts (Java, 891), catalogue (Go, 1,065), events (Go, 646), fulfillment (Java, 255), orders (Java, 3,042), payment (Go, 542), storefront (JS, 4,991), user (TypeScript, 1,265) — [Source](https://github.com/oracle-quickstart/oci-cloudnative/tree/master/src)
- Pitstop: all C#. CustomerManagementAPI (325 lines), VehicleManagementAPI (286), WorkshopManagementAPI (1,572), WorkshopManagementEventHandler (382), InvoiceService (599), NotificationService (435), AuditlogService (74), TimeService (75), WebApp (1,079) — [Source](https://github.com/EdwinVW/pitstop/tree/main/src)
- YAS: README describes "a pet project aim to practice building a typical microservice application in Java", listing Java 25, Spring Boot 4.0, Next.js and Kafka; top-level directories include cart, customer, inventory, location, media, order, payment, payment-paypal, product, promotion, rating, recommendation, search, tax, webhook, storefront, storefront-bff, backoffice, backoffice-bff — [Source](https://github.com/nashtech-garage/yas)
- Train Ticket: 47 `ts-*` directories at HEAD, 45 of them ending `-service`; README lists Java (Spring Boot), Node.js (Express), Python (Django), Go (Webgo). Papers state 41 or 64 services — [Source](https://github.com/FudanSELab/train-ticket); [RCAEval](https://arxiv.org/pdf/2412.17015)

### Inferences
- The star ranking (eShopOnContainers 24k, Online Boutique 21k, modular-monolith 14k, eShop 11k) reflects age and vendor reach more than fitness as a model; the two archived systems still have very high star counts.
- For FTGO, Robot Shop and Train Ticket, a recent `pushed_at` alongside an old default-branch HEAD implies activity only on side branches (bots or forks merged elsewhere); treat them as unmaintained for practical purposes.
- Service-count disagreements in papers come mostly from whether databases, queues, load generators and optional services are counted. For Online Boutique the README supports 11 including the load generator, and the directory listing supports 12 including the optional shopping assistant.

### Gaps
- Latest release dates for eShop, FTGO, flowing-retail, MuShop, Pitstop, YAS and Train Ticket were not checked (the GitHub API rate limit was exhausted).
- Star counts for the individual Sock Shop service repos come from the organisation page via a summarising fetch, not the API; treat them as approximate.
- Dapr quickstarts and the metadata-only repos were not opened; their structure is unverified.
- eShopOnContainers `dev` branch was not cloned (661 MB); no per-service sizes were obtained.
- No commit counts or contributor counts were collected.

## 2. How contracts between services are defined, where they live, who owns them

### Takeaway
Three distinct patterns exist: one shared protobuf file at the repo root with copies or generated stubs inside each service (Online Boutique, OTel Demo); one OpenAPI file per service inside that service's directory, with consumers generating clients (AWS Retail Store, FTGO); and nothing machine-readable, with event classes duplicated by hand in each consumer (eShop) or plain REST with no schema (Robot Shop, flowing-retail, AKS Store Demo).

### Cited Findings
- Online Boutique: the canonical contract is `protos/demo.proto` (262 lines) at the repo root, defining 9 gRPC services (CartService, RecommendationService, ProductCatalogService, ShippingService, CurrencyService, PaymentService, EmailService, CheckoutService, AdService) — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/protos/demo.proto)
- Online Boutique: copies of the proto also sit inside service directories (`src/currencyservice/proto/demo.proto`, `src/paymentservice/proto/demo.proto`, `src/adservice/src/main/proto/demo.proto`, `src/cartservice/src/protos/Cart.proto`); each service has a `genproto.sh`, and generated stubs are committed (for example `demo_pb2.py` in emailservice, a `genproto` directory in checkoutservice) — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/src)
- OTel Demo: a single `pb/demo.proto` (315 lines) at the repo root; it has the same nine services as Online Boutique plus a FeatureFlagService. No per-service copies exist apart from a health-check proto in `src/currency` — [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/pb/demo.proto)
- OTel Demo: stubs are generated by `make generate-protobuf` (`ide-gen-proto.sh`) or `make docker-generate-protobuf`; `make clean` removes `src/{checkout,product-catalog}/genproto/oteldemo/` and `src/frontend/protos/demo.ts` — [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/Makefile)
- OTel Demo also has a second kind of contract: a `telemetry-schema/` OpenTelemetry Weaver registry defining custom attributes and metrics, enforced in CI by a "Weaver check" job, so "a definition that is invalid or missing from the schema fails the build" — [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/AGENTS.md)
- eShop: the only proto is `src/Basket.API/Proto/basket.proto` (32 lines), owned by the Basket service, with a second copy in `src/ClientApp/Services/Basket/Protos/basket.proto` — [Source](https://github.com/dotnet/eShop/blob/main/src/Basket.API/Proto/basket.proto)
- eShop: integration events have no shared schema. Each service keeps its own copy of the event record classes; for example `OrderStatusChangedToPaidIntegrationEvent.cs` exists separately in Ordering.API, Catalog.API, Webhooks.API and WebApp, and `OrderStatusChangedToStockConfirmedIntegrationEvent.cs` in Ordering.API, PaymentProcessor and WebApp. Only the base `IntegrationEvent` class is shared, in `src/EventBus/Events` — [Source](https://github.com/dotnet/eShop/tree/main/src)
- eShop: no OpenAPI files are committed; the only HTTP description is `src/Catalog.API/Catalog.API.http` — [Source](https://github.com/dotnet/eShop/tree/main/src/Catalog.API)
- AWS Retail Store: each service owns an `openapi.yml` in its own directory (`src/catalog`, `src/cart`, `src/orders`, `src/checkout`, `src/recommendations`); cart, checkout and orders have a `scripts/generate-openapi-spec.sh`, so the spec is generated from code — [Source](https://github.com/aws-containers/retail-store-sample-app/tree/main/src)
- AWS Retail Store: the checkout service holds a generated client for the orders API at `src/checkout/src/clients/orders` (with `.openapi-generator` marker files), so the consumer owns generated client code derived from the provider's spec — [Source](https://github.com/aws-containers/retail-store-sample-app/tree/main/src/checkout)
- FTGO: contracts are split into sibling Gradle modules per service: `*-service-api` (Java message and command classes), `*-service-api-spec` (Swagger JSON, for consumer and restaurant services), and `*-service-contracts` (Spring Cloud Contract Groovy files, 18 to 67 lines each). One gRPC proto exists at `ftgo-order-service/src/main/proto/OrderService.proto` — [Source](https://github.com/microservices-patterns/ftgo-application)
- FTGO: the README requires building contracts first with `./gradlew buildContracts` — [Source](https://github.com/microservices-patterns/ftgo-application/blob/master/README.adoc)
- Sock Shop: design doc says API "specifications are under development"; the main repo's `openapi/README.md` describes OpenAPI (Swagger 2.0) specs per service tested with Dredd — [Source](https://github.com/microservices-demo/microservices-demo/blob/master/openapi/README.md). Conflict: the `openapi/` directory at HEAD contains only `Dockerfile`, `package.json` and `README.md`, with no spec files — [Source](https://github.com/microservices-demo/microservices-demo/tree/master/openapi)
- TeaStore: shared Java entity classes live in an `interfaces/tools.descartes.teastore.entities` module used by all services — [Source](https://github.com/DescartesResearch/TeaStore/tree/master/interfaces)
- No `.proto`, OpenAPI, Swagger, Avro, AsyncAPI or Pact files were found in Spring PetClinic Microservices, flowing-retail, Robot Shop, AKS Store Demo or Bank of Anthos — [PetClinic](https://github.com/spring-petclinic/spring-petclinic-microservices); [flowing-retail](https://github.com/berndruecker/flowing-retail); [Robot Shop](https://github.com/instana/robot-shop); [AKS Store Demo](https://github.com/Azure-Samples/aks-store-demo); [Bank of Anthos](https://github.com/GoogleCloudPlatform/bank-of-anthos)

### Inferences
- For a multi-agent setting where each agent owns one service, the two patterns create different coordination problems. A root-level shared proto (Online Boutique, OTel Demo) has no single owner, so any contract change is a shared-file edit. Per-service OpenAPI with consumer-side generated clients (AWS Retail Store) gives each contract a clear owner and makes the consumer's regeneration step an explicit cross-service action.
- eShop's duplicated event classes are the clearest example of an implicit contract: a field rename in the publisher compiles everywhere and only fails at runtime. That is a realistic source of cross-service coordination tasks.
- None of the systems inspected has a machine-readable schema for its events (no AsyncAPI or Avro). OTel Demo's Kafka payload appears to reuse a protobuf message from `demo.proto`, but I did not confirm the payload type in the consumer code.
- FTGO is the only one found with consumer-driven contract tests as first-class modules.

### Gaps
- Whether Sock Shop's per-service repos carry their own API spec files was not checked.
- CODEOWNERS files were not inspected in any repo, so "who owns the contract" is inferred from file location, not from stated ownership rules.
- Dapr quickstarts, YAS, MuShop, Pitstop and Train Ticket were not searched for contract files in detail.

## 3. Communication style: synchronous vs event-driven

### Takeaway
Online Boutique is purely synchronous gRPC. The OTel Demo is mostly gRPC with some HTTP and one Kafka topic (`orders`) fanning out to two consumers. eShop is the most event-driven of the mainstream ones: three synchronous edges from the web app, and everything in the order lifecycle running over RabbitMQ integration events.

### Cited Findings
- Online Boutique: all nine service interfaces are gRPC services in one proto; the README describes checkoutservice as one that "retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification". No message broker appears in the service table; cartservice uses Redis — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/README.md)
- OTel Demo: per the architecture diagram, gRPC is used for frontend to ad, cart, currency, checkout, product-catalog, recommendation; checkout to cart, currency, payment, product-catalog; recommendation to product-catalog; and most services to flagd. HTTP is used for checkout to email, checkout to shipping, frontend to shipping, shipping to quote. Checkout to Kafka and Kafka to accounting and fraud-detection are labelled TCP — [Source](https://opentelemetry.io/docs/demo/architecture/)
- OTel Demo: the checkout service publishes to a Kafka topic that defaults to `orders` (overridable by `KAFKA_TOPIC`) and only if `KAFKA_ADDR` is set; the accounting consumer reads the same default topic — [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/src/checkout/kafka/producer.go); [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/src/accounting/Consumer.cs)
- OTel Demo: Kafka, accounting and fraud-detection are defined in a separate `compose.full.yaml`; minimal mode leaves them out — [Source](https://opentelemetry.io/docs/demo/docker-deployment/)
- eShop synchronous calls: WebApp registers a gRPC client for Basket (`http://basket-api`) and typed HTTP clients for Catalog (`catalog-api`) and Ordering (`ordering-api`); WebhookClient has an HTTP client for `webhooks-api` — [Source](https://github.com/dotnet/eShop/blob/main/src/WebApp/Extensions/Extensions.cs)
- eShop event subscriptions (RabbitMQ): Basket.API subscribes to OrderStarted; Catalog.API to OrderStatusChangedToAwaitingValidation and OrderStatusChangedToPaid; Ordering.API to GracePeriodConfirmed, OrderPaymentFailed, OrderPaymentSucceeded, OrderStockConfirmed, OrderStockRejected; PaymentProcessor to OrderStatusChangedToStockConfirmed; Webhooks.API to OrderStatusChangedToPaid, OrderStatusChangedToShipped, ProductPriceChanged; WebApp to six OrderStatusChanged events — [Source](https://github.com/dotnet/eShop/tree/main/src)
- eShop infrastructure, from the AppHost: Redis, RabbitMQ (named `eventbus`), and one PostgreSQL server with four databases (catalogdb, identitydb, orderingdb, webhooksdb) — [Source](https://github.com/dotnet/eShop/blob/main/src/eShop.AppHost/AppHost.cs)
- eShopOnContainers: client apps talk to microservices over HTTP; services share updates through integration events on an event bus that can be RabbitMQ or Azure Service Bus — [Source](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev)
- Sock Shop: "All services communicate using REST over HTTP. This was chosen due to the simplicity of development and testing" — [Source](https://github.com/microservices-demo/microservices-demo/blob/master/internal-docs/design.md)
- AWS Retail Store: REST between services (UI is configured with endpoints for catalog, carts, orders, checkout; checkout with an orders endpoint, falling back to a mock if empty). The orders service publishes events through a configurable provider: `in-memory`, `sqs` or `rabbitmq`, default in-memory — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/src/orders/README.md); [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/src/checkout/README.md)
- FTGO: "The services have a REST API" and "also communicate using the Apache Kafka message broker via the Eventuate Tram framework"; the order service runs CreateOrder, CancelOrder and ReviseOrder sagas — [Source](https://github.com/microservices-patterns/ftgo-application/blob/master/README.adoc)
- Robot Shop: cart calls catalogue over HTTP; payment calls user and cart over HTTP; dispatch (Go) connects to RabbitMQ via AMQP — [Source](https://github.com/instana/robot-shop)
- TeaStore: "Services communicate using REST and using the Netflix Ribbon client side load balancer" — [Source](https://github.com/DescartesResearch/TeaStore/blob/master/README.md)
- AKS Store Demo: RabbitMQ is "for an order queue"; makeline-service "handles processing orders from the queue and completing them" — [Source](https://github.com/Azure-Samples/aks-store-demo/blob/main/README.md)
- Train Ticket is described in one paper as featuring both synchronous and asynchronous communication — [RCAEval](https://arxiv.org/pdf/2412.17015)

### Inferences
- The OTel Demo's shape (synchronous checkout orchestration, then one event topic consumed by independent downstream services) maps directly onto a Storefront to Orders to (Billing, Notifications) design, where Billing and Notifications would be event consumers.
- eShop shows the richer alternative: an order state machine where each state change is an event and several services react. It gives more cross-service change scenarios but needs a broker and an outbox table.
- AWS Retail Store's "in-memory by default, broker optional" switch is a useful trick for keeping a seed codebase runnable without containers.

### Gaps
- The Kafka message payload type in the OTel Demo was not confirmed in consumer code.
- Sock Shop's queue path (shipping to RabbitMQ to queue-master) was not verified from a page I opened; the design doc only states REST.
- flowing-retail, MuShop, YAS and Pitstop event topologies were not traced.

## 4. Testing and local build/run weight

### Takeaway
Test depth is thin in the polyglot demos: Online Boutique's CI runs only Go tests and the C# cart tests, and the OTel Demo relies on whole-system telemetry and Cypress tests instead of per-service unit tests. eShop, FTGO and AWS Retail Store have the most complete layered testing. Every system needs Docker to run in full; the OTel Demo states about 6 GB RAM and 14 GB disk.

### Cited Findings
- Online Boutique: PR and main CI workflows run `go test` and `dotnet test src/cartservice/`; no pytest, npm test or Gradle test steps were found in the workflows — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/.github/workflows/ci-pr.yaml)
- Online Boutique: test files exist only in the Go services and cartservice (test-ish lines: frontend 430, checkoutservice 245, shippingservice 206, cartservice 160, productcatalogservice 101; zero in the Python, Node.js and Java services) — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/src)
- Online Boutique local run: requires Docker, kubectl and skaffold 2.0.2+, on Minikube (at least 4 CPUs, 4.0 GiB memory, 32 GB disk), Kind, or Docker Desktop Kubernetes (at least 3 CPUs, 6.0 GiB memory); there is no Docker Compose path in the development guide — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/docs/development-guide.md)
- OTel Demo: `test/telemetry` holds a Python test suite run against the whole running demo (`test_traces.py`, `test_traces_edges.py`, `test_metrics.py`, `test_logs.py`, `test_collector.py`, `test_agentic.py`); `make run-telemetry-tests` starts the demo and waits a default 240-second warm-up; the frontend has Cypress end-to-end tests run by `make run-frontend-tests` — [Source](https://github.com/open-telemetry/opentelemetry-demo/blob/main/Makefile)
- OTel Demo: unit-style test files exist in only a few services (checkout 362 lines, recommendation 297, cart 220, product-catalog 90, flagd-ui 847) — [Source](https://github.com/open-telemetry/opentelemetry-demo/tree/main/src)
- OTel Demo local run: Docker with Compose v2.0.0+; about 6 GB RAM for the full application or about 3 GB in minimal mode; about 14 GB disk; `make start` or `make start-minimal` — [Source](https://opentelemetry.io/docs/demo/docker-deployment/)
- eShop: `tests/` has Basket.UnitTests, Ordering.UnitTests (945 lines), ClientApp.UnitTests, Application.UnitTests, eShop.AppHost.UnitTests, and functional tests for Basket, Catalog (575 lines), Ordering and Webhooks; an `e2e/` directory has three Playwright specs (browse, cart, checkout) — [Source](https://github.com/dotnet/eShop/tree/main/tests)
- eShop: "Functional tests in this leverage the Aspire host to spin up test containers and require that Docker be running" — [Source](https://github.com/dotnet/eShop/blob/main/tests/README.md)
- eShop local run: .NET 10 SDK, the Aspire CLI, and an OCI container runtime (Docker Desktop recommended, Podman supported); start with `aspire run` — [Source](https://github.com/dotnet/eShop/blob/main/README.md)
- eShopOnContainers local run: `docker-compose build` then `docker-compose up` from `/src` — [Source](https://github.com/dotnet-architecture/eShopOnContainers/tree/dev)
- Sock Shop: the testing doc defines five levels (unit, component, container, application, user), with contract checks placed at the component level — [Source](https://github.com/microservices-demo/microservices-demo/blob/master/internal-docs/testing.md)
- AWS Retail Store: an Nx monorepo with uniform targets per component: `yarn nx test` (unit), `yarn nx test:integration`, `yarn nx serve`, `yarn nx container`; `yarn nx run-many -t test --projects=tag:service` runs all services; a Cypress `src/e2e` suite and an `e2e-test.yml` workflow exist — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/DEVELOPER_GUIDE.md)
- AWS Retail Store local run: only Docker is needed; download the release `docker-compose.yaml` and run `docker compose up` with a `DB_PASSWORD` — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/README.md)
- FTGO: has a dedicated `ftgo-end-to-end-tests` module (405 lines), per-service contract modules, and the heaviest unit test body in order-service (about 1,800 test-ish lines); README says it "requires a lot of memory. It runs well, for example, on a 16GB Macbook pro" and deploys MySQL and Kafka in Docker — [Source](https://github.com/microservices-patterns/ftgo-application/blob/master/README.adoc)
- Robot Shop and flowing-retail: no test files were found by path name in any service — [Robot Shop](https://github.com/instana/robot-shop); [flowing-retail](https://github.com/berndruecker/flowing-retail)
- Robot Shop: building from source needs an Instana agent key for the Nginx tracing module — [Source](https://github.com/instana/robot-shop/blob/master/README.md)
- TeaStore: a Cypress `e2e-tests` directory exists alongside Java unit tests concentrated in the image (2,192 test-ish lines) and recommender (1,188) services — [Source](https://github.com/DescartesResearch/TeaStore)
- Pitstop: separate unit test projects for InvoiceService, NotificationService and WorkshopManagement, plus a UITest project — [Source](https://github.com/EdwinVW/pitstop/tree/main/src)

### Inferences
- AWS Retail Store's convention (the same four task names in every service regardless of language) is the most directly reusable idea for a four-language seed repo: an agent or a grader can run `test` on any service without knowing its toolchain.
- The OTel Demo's edge-level trace tests (`test_traces_edges.py`) are an example of verifying the service graph itself, which could double as a cross-service acceptance check in an RL environment.
- A seed repo that wants fast, deterministic episodes should avoid the Kubernetes-only path of Online Boutique and the 240-second warm-up of the OTel Demo; in-memory defaults and per-service unit tests are what keep the lighter systems quick.

### Gaps
- No build or test was run, so wall-clock build times are unknown for every system.
- Toolchain versions per service (Go, Node, JDK, Python versions) were not recorded except eShop's .NET SDK.
- I did not confirm what the AWS Retail Store integration tests need (likely containers, but unverified).

## 5. Closest to a TypeScript/Node + Java + C# + Python mix; smallest and most imitable services

### Takeaway
No system has exactly those four languages as its only service languages, but two contain all four: the OTel Demo (TypeScript frontend, Java, C#, Python, plus eight other languages) and Online Boutique (Node.js in plain JavaScript, Java, C#, Python, plus Go). Online Boutique has the smallest, most imitable services (about 240 to 870 lines each); AWS Retail Store has the cleanest per-service ownership and uniform tooling, but no C# or Python.

### Cited Findings
- Online Boutique covers Node.js (currencyservice, paymentservice), Java (adservice), C# (cartservice) and Python (emailservice, recommendationservice), with Go for the remaining four services and the frontend. The Node.js services are JavaScript, not TypeScript — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/README.md)
- OTel Demo covers TypeScript (frontend, React Native app), Java (ad), C#/.NET (accounting, cart) and Python (agent, chatbot, MCP, load generator, and recommendation as of release 3.1.0), alongside Go, C++, Ruby, Kotlin, PHP, Rust, Elixir and JavaScript — [Source](https://opentelemetry.io/docs/demo/architecture/)
- In the OTel Demo, the roles nearest the seed company's are in the right languages already: storefront in TypeScript (frontend), accounting (billing-like, Kafka consumer) in C#, and email in Ruby (a 102-line single file) — [Source](https://github.com/open-telemetry/opentelemetry-demo/tree/main/src)
- Online Boutique's emailservice (the notifications analogue) is Python, 280 lines in 3 files; its paymentservice is Node.js, 294 lines in 4 files; its cartservice is C#, 868 lines in 9 files; its adservice is Java, 354 lines in 2 files — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/src)
- AWS Retail Store has an Orders service in Java (2,563 lines) and a Checkout service in TypeScript on Node (2,765 lines), matching two of the four target roles and languages, but nothing in C# or Python — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/README.md)
- Sock Shop had an alternate C# implementation of orders (`orders.NET`) beside the Java one, plus Go and Node; no Python service — [Source](https://github.com/orgs/microservices-demo/repositories?type=all)
- Robot Shop has Node.js, Java, Python, Go and PHP, with no C#; three of its services are single files of 188 to 407 lines — [Source](https://github.com/instana/robot-shop)
- AKS Store Demo has JavaScript, Go, Rust, Vue/TypeScript and Python; no Java or C# — [Source](https://github.com/Azure-Samples/aks-store-demo/blob/main/README.md)
- eShop and Pitstop are single-language C#; PetClinic Microservices, FTGO, flowing-retail, TeaStore are single-language Java (FTGO has one JS gateway) — [eShop](https://github.com/dotnet/eShop); [PetClinic](https://github.com/spring-petclinic/spring-petclinic-microservices)
- eShop's PaymentProcessor is 72 lines in 7 files and OrderProcessor 176 lines in 7 files, the smallest event-driven workers seen — [Source](https://github.com/dotnet/eShop/tree/main/src)

### Inferences
- Best single structural model for a four-service seed: Online Boutique for service size and the shared-proto layout, or AWS Retail Store for per-service contract ownership, uniform task names and an in-memory default. A hybrid is reasonable: Retail Store's repo layout and tooling conventions, Online Boutique's service size, and the OTel Demo's "checkout publishes an order event, billing-like and notification-like services consume it" topology.
- The OTel Demo is the closest language match on paper but a poor size model as a whole: about 20 services, 12 languages and a large observability stack. Individual services in it are still small enough to study.
- eShop is the best model for the Billing (C#) service's internals and for event-driven order state, even though it offers nothing on polyglot concerns.
- Licence position for "read but do not copy": all of the main candidates are permissive (Apache-2.0, MIT, MIT-0, UPL-1.0). The two with unclear GitHub licence detection are FTGO (Apache-2.0 text in `LICENSE.md` with an Eventuate copyright line) and eShopOnContainers (MIT on the `dev` branch only). Apache-2.0 carries notice and attribution duties if any code were copied; MIT-0 has none.

### Gaps
- I did not find any public reference app whose service languages are exactly TypeScript, Java, C# and Python. Absence here means not found in the roughly 30 repos checked, not proven absent.
- Dapr quickstarts and similar tutorial collections contain multi-language samples of the same small service, which could be closer per-language templates, but they were not opened.

## 6. Service graphs (who calls whom)

### Takeaway
The dominant shape is a frontend or gateway fanning out to leaf services, with one orchestrating "checkout" or "ordering" service in the middle. The OTel Demo and eShop add an event tail after the order is placed.

### Cited Findings
- OTel Demo (from the official diagram): Internet, load-generator and the React Native app call frontend-proxy (Envoy) over HTTP. Frontend-proxy routes to frontend, image-provider, flagd-ui and chatbot. Frontend calls ad, cart, currency, checkout, product-catalog and recommendation over gRPC and shipping over HTTP. Checkout calls cart, currency, payment and product-catalog over gRPC, email and shipping over HTTP, and writes to Kafka. Shipping calls quote over HTTP. Recommendation calls product-catalog over gRPC. Cart uses a Valkey cache; product-catalog and accounting use PostgreSQL. Kafka feeds accounting and fraud-detection. Chatbot calls agent; agent calls frontend and MCP; MCP calls frontend. Most services call flagd for feature flags — [Source](https://opentelemetry.io/docs/demo/architecture/)
- eShop (from code): WebApp calls Basket.API (gRPC), Catalog.API (HTTP) and Ordering.API (HTTP), and references Identity.API for sign-in. WebhookClient calls Webhooks.API. Ordering.API publishes order status events; OrderProcessor publishes GracePeriodConfirmed back to Ordering.API; Catalog.API consumes AwaitingValidation and replies with stock confirmed or rejected; PaymentProcessor consumes StockConfirmed and replies with payment succeeded or failed; Basket.API consumes OrderStarted; Webhooks.API consumes Paid, Shipped and ProductPriceChanged; WebApp consumes all status changes for live UI updates — [Source](https://github.com/dotnet/eShop/blob/main/src/eShop.AppHost/AppHost.cs); [Source](https://github.com/dotnet/eShop/tree/main/src)
- Online Boutique: the proto defines the callable surface (cart, recommendation, product catalog, shipping, currency, payment, email, checkout, ad); the README states checkout orchestrates cart retrieval, payment, shipping and the email notification, and that the load generator sends requests to the frontend — [Source](https://github.com/GoogleCloudPlatform/microservices-demo/blob/main/README.md)
- AWS Retail Store: UI calls catalog, carts, orders and checkout (four configured endpoints); checkout calls orders; orders publishes events to an optional broker — [Source](https://github.com/aws-containers/retail-store-sample-app/blob/main/src/checkout/README.md)
- Robot Shop (from code and compose): web (Nginx) fronts the services; cart calls catalogue; payment calls user and cart; dispatch consumes from RabbitMQ; catalogue and user depend on MongoDB, cart and user on Redis, shipping and ratings on MySQL — [Source](https://github.com/instana/robot-shop/blob/master/docker-compose.yaml)
- AKS Store Demo: store-front places orders through order-service, which queues them in RabbitMQ; makeline-service processes the queue and persists to the database; store-admin views queued orders and manages products through product-service; virtual-customer and virtual-worker simulate load — [Source](https://github.com/Azure-Samples/aks-store-demo/blob/main/README.md)
- Bank of Anthos: frontend serves the site; user-service signs JWTs "used for authentication by other services"; ledger-writer validates and writes transactions; balance-reader and transaction-history are read caches over ledger-db — [Source](https://github.com/GoogleCloudPlatform/bank-of-anthos/blob/main/README.md)
- FTGO: an API gateway fronts consumer, restaurant, order, kitchen, accounting, delivery and order-history services; the gateway "uses API composition to implement the REST endpoint for retrieving the order history"; order-service coordinates the others through sagas over Kafka — [Source](https://github.com/microservices-patterns/ftgo-application/blob/master/README.adoc)
- TeaStore: five services (webui, auth, image, persistence, recommender) register with a registry and call each other over REST — [Source](https://github.com/DescartesResearch/TeaStore/blob/master/README.md)

### Inferences
- Online Boutique's full edge list, as commonly drawn: frontend calls product catalog, currency, cart, recommendation, shipping, checkout and ad; checkout calls cart, product catalog, currency, shipping, payment and email; recommendation calls product catalog. This matches the OTel Demo diagram (which descends from the same codebase, as the near-identical proto shows), but I did not parse Online Boutique's architecture image or its `rpc.go`, so treat the exact list as likely rather than verified.
- The near-identical proto service lists show the OTel Demo is a fork lineage of Online Boutique that later added Kafka, feature flags and extra languages.
- A four-service seed maps most naturally onto: Storefront calls Orders synchronously; Orders emits an order event; Billing consumes it and emits a payment result; Notifications consumes order and payment events. That is the eShop payment loop shrunk to four nodes.
- PetClinic Microservices is gateway to three domain services plus config and discovery servers; this is inferred from module names, not traced.

### Gaps
- Sock Shop's edge list was not verified from an opened page (the architecture diagram is an image on an archived site). The commonly cited graph (front-end to catalogue, carts, user, orders; orders to carts, user, payment, shipping; shipping to RabbitMQ to queue-master) is from general knowledge only.
- MuShop, YAS, Pitstop, flowing-retail and Train Ticket graphs were not traced.
- eShop's Identity.API interactions and the mobile BFF route were not traced in detail.
