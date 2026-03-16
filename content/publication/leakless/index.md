---
title: "LeakLess: Selective Data Protection Against Memory Leakage Attacks for Serverless Platforms"
authors: ["admin", "Seyedhamed Ghavamnia", "Michalis Polychronakis"]
date: 2025-02-28

publication_types: ["1"]
publication: "In Proceedings of the Network and Distributed System Security Symposium (NDSS). San Diego, CA"
publication_short: ""

abstract: "As the use of language-level sandboxing for running untrusted code grows, the risks associated with memory disclosure vulnerabilities and transient execution attacks become increasingly significant. In this paper we present LeakLess, a selective data protection approach for serverless computing platforms. LeakLess alleviates the limitations of previous selective data protection techniques by combining in-memory encryption with a separate I/O module to enable the safe transmission of the protected data between serverless functions and external hosts. We implemented LeakLess on top of the Spin serverless platform and evaluated it with real-world serverless applications. Our results demonstrate that LeakLess offers robust protection while incurring a minor throughput decrease of up to 2.8% when the I/O module runs on a different host than the Spin runtime, and up to 8.5% when it runs on the same host."

tags: ["Serverless Security", "Transient Execution Attacks", "Selective Data Protection", "WebAssembly", "Memory Disclosure", "Spectre", "Meltdown"]
categories: []
featured: true

url_pdf: files/leakless.pdf
url_code: https://github.com/mrostamipoor/LeakLess
url_dataset: https://github.com/mrostamipoor/LeakLess/tree/main/leakless-dataset

image:
  caption: ""
  focal_point: ""
  preview_only: true

slides: ""
---

## The Problem

Serverless FaaS platforms such as Cloudflare Workers and Fastly have moved away from per-tenant process isolation toward **language-level sandboxing** (WebAssembly) to run multiple customers' functions within a single process. While this dramatically improves density and cold-start latency, it weakens isolation guarantees: bugs in the JavaScript or WebAssembly runtime itself can expose secrets across tenants.

Two classes of attacks exploit this gap:

- **Memory disclosure vulnerabilities** — out-of-bounds reads in the V8/Wasm runtime can expose the in-memory plaintext of other tenants' sensitive data.
- **Transient execution attacks (Spectre/Meltdown)** — a malicious co-located function can mount Spectre-BTI or Spectre-BCB attacks to leak secrets from the same address space, even when memory safety guarantees are nominally in place.

Vendor mitigations (disabling timer APIs, memory shuffling) are incomplete and cannot provide future-proof protection. Process isolation would restore security but eliminates all the performance benefits of language-level sandboxing.

## Key Insight

Rather than trying to prevent every possible leakage path — a losing battle as new Spectre variants continue to emerge — LeakLess **accepts that data in memory may leak, but ensures leaked data is always encrypted and therefore useless to the attacker**.

Any sensitive value that leaves memory (via a memory disclosure or a transient execution side channel) will be ciphertext. The cryptographic keys never reside in the serverless runtime's address space.

## Design

LeakLess introduces a dedicated **I/O module** that runs as a separate process (optionally on a separate VM or physical host) and acts as a cryptographic proxy between serverless functions and backend services.

{{< figure src="featured.png" title="LeakLess architecture: sensitive data stays encrypted in the serverless runtime's address space. The I/O module holds the keys and handles all plaintext operations." >}}

**Sensitive data annotation** requires minimal developer effort:

- *Source code annotation:* Developers mark sensitive variables with `#[LEAKLESS_SECRET]` (Rust) or `//#[LEAKLESS_SECRET]` (Go). The compiler/directive replaces the value with its encrypted form.
- *Configuration file annotation:* Secrets defined in platform configuration files or secrets management APIs are annotated with the `leakless_secret` option — no code changes required.

**Data flow protection:**

1. Outgoing sensitive data is transmitted with the `LEAKLESS_` prefix (encrypted ciphertext). The I/O module intercepts the request, decrypts the value, and forwards the plaintext to the backend.
2. Incoming sensitive data (e.g., a user's credit card number) is annotated by client-side JS with the `LEAKLESS_` prefix before transmission. When the I/O module receives the request, it identifies values carrying this prefix as sensitive, encrypts them, and preserves the `LEAKLESS_` prefix on the encrypted value before forwarding the request to the serverless function — so plaintext never enters the runtime's address space.

This design provides protection against **intra-process**, **cross-process**, and **user-to-kernel** transient execution attacks by varying the deployment topology of the I/O module.

## Results

We collected **1,074 publicly available serverless applications** from GitHub and assessed their use of sensitive data:

| Metric | Value |
|---|---|
| Apps containing at least one type of sensitive data | 449 / 1,074 (42%) |
| Apps fully supported by LeakLess | 407 / 449 **(91%)** |
| Apps partially supported | 33 / 449 (7%) |
| Throughput overhead (I/O module on separate host) | **≤ 2.8%** |
| Throughput overhead (I/O module on same host) | **≤ 8.5%** |

Sensitive data types observed across the dataset include authentication secrets, request signing keys, database credentials, and user passwords. LeakLess was experimentally validated with six real-world, widely-used serverless applications under stress-testing conditions.

## Venue

**Network and Distributed System Security (NDSS) Symposium 2025**
February 24–28, 2025 · San Diego, CA, USA
ISBN 979-8-9894372-8-3 · DOI: [10.14722/ndss.2025.230035](https://dx.doi.org/10.14722/ndss.2025.230035)
