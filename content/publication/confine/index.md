---
title: "Confine: Fine-grained System Call Filtering for Container Attack Surface Reduction"
authors: ["admin", "Seyedhamed Ghavamnia", "Michalis Polychronakis"]
date: 2023-09-01

publication_types: ["2"]
publication: "In Computers & Security, vol. 132, September 2023"
publication_short: ""

abstract: "Reducing the attack surface of the OS kernel is a promising defense-in-depth approach for mitigating the fragile isolation guarantees of container environments. In contrast to hypervisor-based systems, malicious containers can exploit vulnerabilities in the underlying kernel to fully compromise the host and all other containers running on it. Previous container attack surface reduction efforts have relied on dynamic analysis and training using representative workloads to limit the set of system calls exposed to containers. These approaches, however, do not capture exhaustively all the code that can potentially be needed by future workloads or rare runtime conditions. Aiming to provide a practical solution for the protection of arbitrary containers, we present Confine, a generic approach for the automated generation of restrictive system call policies for Docker containers. Confine uses static code analysis to inspect the containerized application and all its dependencies, identify the superset of system calls required for the correct operation of the container, and generate both a container-wide and application-specific Seccomp system call policy that can be readily enforced while loading the container and launching the main program. The results of our experimental evaluation with a set of 27 Docker images show that applying container-wide filtering disables more than 145 system calls on average across the entire container, and application-specific filtering increases the number of filtered system calls by 25% on average."

tags: ["Container Security", "Attack Surface Reduction", "System Call Filtering", "Static Analysis", "Seccomp", "Debloating", "Docker", "Linux Kernel"]
categories: []
featured: true

url_pdf: files/confine.pdf
url_code: https://github.com/mrostamipoor/Confine_Plus
url_dataset: https://github.com/mrostamipoor/confine/blob/master/images.json

image:
  caption: ""
  focal_point: ""
  preview_only: true

slides: ""
---

## The Problem

Containers rely on OS-level virtualization: they share the host kernel, relying on namespaces, cgroups, and capabilities for isolation. Unlike VMs, a vulnerability in the Linux kernel exploited from within a container can **fully compromise the host and every other container** on it.

The Linux kernel's attack surface has grown dramatically — from 126 system calls in kernel 1.0 (1991) to **335 system calls** in kernel 5.4. Most containerized applications use only a small fraction of these. Every unused system call is an unnecessary entry point to kernel code that could be exploited.

**Seccomp BPF** allows restricting the set of system calls available to a container, but generating correct policies is challenging:

- *Dynamic analysis* (the dominant prior approach) instruments the container under representative workloads and allows only observed system calls. It **misses calls along untrained code paths** — for example, calls only triggered during cache eviction, error handling, or rare initialization sequences.
- Manual policy writing is error-prone and does not scale across container images.

## Key Insight

By relying on **static binary analysis** — inspecting all execution paths rather than only those exercised during training — Confine can guarantee a sound (complete) system call superset that will never block legitimate application behavior, while still filtering far more calls than dynamic approaches.

## Design

Confine operates in three phases:

{{< figure src="featured.png" title="Confine's processing pipeline: a one-time dynamic phase identifies running processes; static analysis then derives the complete system call superset for both container-wide and application-specific policies." >}}

**Phase 1 — Identify running applications (dynamic, one-time):**
A lightweight profiling pass launches the container and records every process spawned during a 30-second initialization window. This captures utility programs (bash, init scripts) that run only at startup — without requiring application-specific workloads.

**Phase 2 — Static analysis (per container image):**
- *Libc function → system call mapping:* Confine builds a precise callgraph of libc at the source level, mapping each exported wrapper to the kernel system calls it may invoke, including through complex internal call chains (e.g., `fgets → __mmap → mmap`).
- *Direct syscall extraction:* Applications and libraries that invoke `syscall()` or the `syscall` assembly instruction directly are identified via binary disassembly.
- A **container-wide policy** is derived as the union of system calls needed by all processes.
- An **application-specific policy** is then generated for the main long-running program, removing calls only needed during initialization.

**Phase 3 — Argument concretization:**
For system calls that cannot be filtered entirely, Confine restricts their **argument values** via intra-procedural reaching definitions analysis. This prevents, for example, passing dangerous flag combinations to `mmap`, `open`, or `prctl` — blocking many CVE exploitation paths even when the system call itself is permitted.

## Results

Evaluated on **27 publicly available Docker images** (nginx, Redis, MongoDB, Apache, etc.):

| Metric | Result |
|---|---|
| System calls disabled by container-wide filtering | **145+ per container on average** (out of 335) |
| Additional calls removed by application-specific filtering | **+25% on average** |
| Linux kernel CVEs mitigated via argument concretization | **28 CVEs** |
| Containers where functionality was broken | **0** |

A notable case study: dynamic analysis of nginx misses the `unlink` system call — used only when the cache fills and old files must be deleted — because this path is never triggered during training. Confine's static analysis correctly identifies `unlink` as required and includes it in the policy, preventing false denials in production.

## Venue

**Computers & Security**, Volume 132, September 2023, Article 103325
Elsevier · DOI: [10.1016/j.cose.2023.103325](https://doi.org/10.1016/j.cose.2023.103325)
Received: 21 December 2022 · Revised: 30 May 2023 · Accepted: 5 June 2023
