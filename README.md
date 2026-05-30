# ShopBridge × UCP Demo

A comprehensive single-page demo that documents and simulates core **Universal Commerce Protocol (UCP)** commerce flows in a portfolio-style UI.

---

## 1) Purpose of this repository

This project demonstrates how an agentic commerce platform can integrate with merchant systems using UCP concepts from [ucp.dev](https://ucp.dev).  
It is designed as an educational and presentation artifact, not a production backend.

This demo helps you understand:
- how capabilities are discovered and negotiated,
- how checkout and identity flows are coordinated,
- how payments, transports, security, and versioning affect interoperability.

---

## 2) What this project contains

- `index.html` — complete frontend demo (HTML, CSS, JavaScript in one file).
- `README.md` — documentation for all major sections and protocol concepts used in the demo.

No build pipeline is required for local use.

---

## 3) Run locally

### Option A: open directly
1. Clone the repository.
2. Open `/tmp/workspace/Yash121l/ucp-demo/index.html` in a browser.

### Option B: run a simple local server
```bash
cd /tmp/workspace/Yash121l/ucp-demo
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

---

## 4) UCP context (high-level)

UCP provides a standard way for platforms (including AI agents), merchants, payment providers, and identity systems to interoperate without building one-off integrations for each pair.

In this demo, UCP ideas are represented through:
- profile discovery,
- capability negotiation,
- cart/checkout/order lifecycle simulation,
- identity linking via OAuth,
- payment handler and mandate flows,
- multi-transport protocol mapping,
- standard error/fallback handling,
- security signals and signature concepts,
- version compatibility checks.

Reference:
- Documentation: https://ucp.dev
- Specification overview: https://ucp.dev/specification/overview
- UCP GitHub: https://github.com/Universal-Commerce-Protocol

---

## 5) Section-by-section documentation

The sidebar in the UI maps to the following sections.

### 5.1 Portfolio Hub (`sec-intro`)
**What it does:** Introduces the ShopBridge architecture and end-to-end demo flow.  
**Protocol impact:** Establishes the integration model: **Agent ↔ UCP bridge ↔ Merchant APIs**.  
**Why it matters:** Gives system context so each protocol feature is interpreted as part of one connected commerce pipeline.

---

### 5.2 UCP Profiles Discovery (`sec-profiles`)
**UI label:** `/.well-known/ucp`  
**What it does:** Displays sample merchant and platform profile documents.  
**Protocol impact:** Profile discovery defines available capabilities, endpoints, key metadata, and supported transports before runtime operations begin.  
**Why it matters:** Without profile discovery, automatic interoperability and safe capability matching are not possible.

---

### 5.3 Capability Negotiation Engine (`sec-negotiation`)
**UI label:** `negotiateCapabilities()`  
**What it does:** Simulates intersection logic between platform and merchant capabilities.  
**Protocol impact:** Performs compatibility filtering:
- shared capability names,
- mutually supported versions,
- pruning of incompatible child extensions.
**Why it matters:** Prevents unsupported operations and ensures both sides execute only mutually valid protocol contracts.

---

### 5.4 Catalog Capability (`sec-catalog`)
**UI label:** `/catalog/search`  
**What it does:** Simulates product discovery and response payload inspection.  
**Protocol impact:** Standardized catalog querying enables agents to search merchant inventory with consistent semantics.  
**Why it matters:** Reliable discovery is the first operational step in agentic commerce and drives downstream cart/checkout accuracy.

---

### 5.5 Cart Capability (`sec-cart`)
**UI label:** `/carts/:id`  
**What it does:** Shows cart state management (line items, quantity updates, promo application).  
**Protocol impact:** Defines a stable mutable cart object shared between platform and merchant contexts.  
**Why it matters:** Cart state integrity directly affects pricing, discounts, taxes, shipping decisions, and checkout success.

---

### 5.6 Checkout Lifecycle Stepper (`sec-checkout`)
**UI label:** `/checkout-sessions`  
**What it does:** Walks through cart review, shipping, payment, and confirmation phases.  
**Protocol impact:** Demonstrates ordered checkout-state transitions and payload visibility at each stage.  
**Why it matters:** Structured lifecycle control reduces ambiguity, improves recoverability, and aligns payment/fulfillment timing.

---

### 5.7 Identity Linking (`sec-identity`)
**UI label:** `/.well-known/oauth-authorization-server`  
**What it does:** Simulates account linking and authorization metadata discovery.  
**Protocol impact:** Uses OAuth-based identity linking so agents can act with scoped user authorization.  
**Why it matters:** Enables secure delegated actions while preserving explicit consent and account-bound access boundaries.

---

### 5.8 Order Lifecycles & Webhooks (`sec-orders`)
**UI label:** `/orders/:id`  
**What it does:** Simulates status progression events (ship, deliver, refund/return).  
**Protocol impact:** Webhook-driven order state notifications keep platforms synchronized with merchant fulfillment updates.  
**Why it matters:** Maintains post-checkout transparency and enables proactive agent behavior (tracking updates, exception handling, returns).

---

### 5.9 Payment Handler Playground (`sec-payments`)
**UI label:** `payment.handlers`  
**What it does:** Demonstrates payment instrument intersection and scenario-based flows:
- wallet-style flows,
- direct tokenization/card + 3DS style handling,
- AP2 mandate-style autonomous payment flow.
**Protocol impact:** Standardized payment handler declarations and intersection logic determine which payment paths are safe and valid for both parties.  
**Why it matters:** Payment compatibility and mandate security are critical for conversion, compliance boundaries, and autonomous transactions.

---

### 5.10 Multi-Transport Configurations (`sec-transports`)
**UI label:** `dev.ucp.shopping.services`  
**What it does:** Compares equivalent operations across REST, MCP (JSON-RPC), A2A, and embedded patterns.  
**Protocol impact:** Shows that payload semantics remain stable while transport layers differ.  
**Why it matters:** Teams can adopt transport methods that fit their architecture without redefining business behavior.

---

### 5.11 Error Simulator & Fallbacks (`sec-errors`)
**UI label:** `UCP standard errors`  
**What it does:** Triggers representative error conditions and fallback continuation behavior.  
**Protocol impact:** Standard error payloads communicate deterministic recovery instructions to agents (retry, fallback, escalate, continue_url handoff).  
**Why it matters:** Robust failure handling is essential for safe automation and user trust.

---

### 5.12 UCP Security & Signals (`sec-security`)
**UI label:** `signals.json`  
**What it does:** Simulates fraud/risk signal generation and message-signature concepts.  
**Protocol impact:** Demonstrates contextual signals, namespace governance, and HTTP Message Signature ideas (RFC 9421 concept in UI) for request authenticity and trust scoring.  
**Why it matters:** Security metadata and signed requests reduce fraud risk and strengthen machine-to-machine confidence.

---

### 5.13 Versioning & Compatibility (`sec-versioning`)
**UI label:** `UCP Versions API`  
**What it does:** Simulates version handshake choices using date-based version strings.  
**Protocol impact:** Negotiates supported protocol versions and clarifies safe vs breaking changes.  
**Why it matters:** Version governance protects interoperability over time and enables controlled evolution of capabilities.

---

## 6) Protocols and standards represented in this demo

This demo references the following protocol families and implementation patterns:

- **UCP capability model** (profiles, negotiation, capability/extension compatibility)
- **Well-known discovery endpoints** for profile and auth metadata exchange
- **OAuth 2.0-style identity linking** for delegated agent authorization
- **Payment interoperability patterns** (tokenization, mandate-oriented flows)
- **Webhook-based order synchronization**
- **Transport mappings** across REST / MCP(JSON-RPC) / A2A / embedded channels
- **Structured error and fallback signaling**
- **HTTP Message Signatures concept** (RFC 9421) for request integrity
- **Date-based protocol version negotiation**

> Note: This repository is a front-end simulation intended for demonstration and learning. It is not a certified conformance suite or production UCP implementation.

---

## 7) How these protocols affect real integrations

In practical integrations, these protocol choices affect:
- **Interoperability:** fewer custom one-off integrations.
- **Security posture:** stronger delegated auth, signed requests, and risk signaling.
- **Operational resilience:** clearer errors, predictable retries, and fallback routing.
- **Scalability:** transport flexibility with consistent semantics.
- **Change management:** explicit version negotiation and compatibility control.

---

## 8) Contributing

Contributions are welcome for:
- improving section-level documentation,
- aligning terminology with latest UCP documentation,
- refining payload examples and explanatory text.

Keep changes focused and consistent with official UCP references where applicable.
