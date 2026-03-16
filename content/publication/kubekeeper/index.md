---
title: "KubeKeeper: Protecting Kubernetes Secrets Against Excessive Permissions"
authors: ["admin", "Aliakbar Sadeghi", "Michalis Polychronakis"]
date: 2025-06-01

publication_types: ["1"]
publication: "In Proceedings of the 10th IEEE European Symposium on Security and Privacy (EuroS&P). Venice, Italy."
publication_short: ""

abstract: "Kubernetes has become the dominant platform for managing containerized applications, but its native Secrets management mechanisms introduce security vulnerabilities, especially in environments where third-party applications may have excessive permissions. In this paper, we present KubeKeeper, a comprehensive solution for protecting Kubernetes Secrets against leakage due to excessive permissions. KubeKeeper automatically encrypts Secrets and ensures that only explicitly authorized Pods can access their decrypted form. This is achieved by integrating with Kubernetes' admission control framework to transparently enforce access policies, without requiring changes to application code and with minimal integration effort into existing cluster infrastructure. We evaluated KubeKeeper on a diverse set of 498 Kubernetes applications and demonstrate that it successfully protects Secrets against all identified excessive permissions, without introducing performance degradation during execution or any significant overhead during Pod creation and deployment."

tags: ["Kubernetes", "Cloud Security", "Secrets Management", "Excessive Permissions", "RBAC", "Admission Control", "Container Security"]
categories: []
featured: true

url_pdf: files/kubekeeper.pdf
url_code: https://github.com/mrostamipoor/KubeKeeper

image:
  caption: ""
  focal_point: ""
  preview_only: true

slides: ""
---

## The Problem

Kubernetes stores sensitive configuration data — API keys, database credentials, TLS certificates — as **Secrets** objects. Despite their name, Kubernetes Secrets have several fundamental security limitations:

- Secrets are stored **unencrypted in etcd** by default. Encryption at rest is opt-in and lacks key rotation and audit logging.
- **RBAC provides only coarse-grained control.** A user or Service Account granted `get` or `list` permissions on Secrets receives access to all their decrypted values. Kubernetes does not prevent Pods from mounting any Secret in their Namespace.
- **Third-party applications frequently ship with insecure default configurations** that grant excessive permissions — cluster-wide Secret access, Pod creation rights, or both.

Our analysis of 498 real-world Kubernetes applications found that **202 (41%) have excessive permissions** that can lead to unauthorized Secret access:

| Exposure Type | Permissions Found | % of Vulnerable Apps |
|---|---|---|
| Direct access via Secret API | 1,866 permissions | 84% |
| Indirect access via resource scheduling | 3,068 permissions | 79% |

A concrete example: a critical vulnerability in the widely deployed `ingress-nginx` Controller (used in over 40% of clusters) allowed an unauthenticated attacker with network access to obtain the Service Account token with cluster-wide Secret access — disclosing every Secret in the cluster.

## Key Insight

Instead of trying to fix RBAC configurations — a fragile, error-prone approach in dynamic environments — KubeKeeper takes a **cryptographic approach**: Secrets are always stored encrypted, and decryption keys are distributed *only to explicitly authorized Pods* at deployment time. Even if RBAC is misconfigured or bypassed, the attacker only sees ciphertext.

## Design

KubeKeeper integrates with Kubernetes through **Admission Webhooks** — no changes to the Kubernetes source code or application code are required.

**Core mechanism:**

1. When a Secret is created, KubeKeeper's Mutating Admission Webhook **encrypts it with a unique per-Secret key** before it is written to etcd.
2. When a Pod is deployed, KubeKeeper identifies which Secrets it is authorized to access, and **distributes decryption keys exclusively to that Pod** during its admission phase.
3. Unauthorized Pods — whether they have direct API access, indirect scheduling control, or node-level access — receive only ciphertext and cannot decrypt it.

**Advantages over native RBAC:**

| Feature | RBAC | KubeKeeper |
|---|---|---|
| Secrets encrypted at rest | ✗ | ✓ |
| Secrets encrypted in transit | ✗ | ✓ |
| Fine-grained per-Pod access control | ✗ | ✓ |
| Protection against compromised components | ✗ | ✓ |
| Protection against misconfigurations | ✗ | ✓ |
| No application source code changes | ✓ | ✓ |
| No runtime performance overhead | ✓ | ✓ |

## Results

KubeKeeper was evaluated on **498 diverse Kubernetes applications** drawn from public repositories, including applications previously studied in the security literature:

- Successfully **protects Secrets against all identified excessive permission types** — direct, indirect via Secret manipulation, indirect via resource scheduling, and indirect via Node manipulation.
- **Zero application runtime overhead** — encryption/decryption happens outside the critical execution path.
- **No significant overhead during Pod creation and deployment.**
- Requires **no changes to application source code** and minimal cluster integration effort.

We also released a companion **YAML scanner tool** that automatically analyzes Kubernetes configuration files to identify excessive permissions — providing a more efficient and reliable alternative to existing manual analysis tools.

## Venue

**10th IEEE European Symposium on Security and Privacy (EuroS&P 2025)**
June 2025 · Venice, Italy
