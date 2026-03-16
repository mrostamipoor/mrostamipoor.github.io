+++
title    = "Research & Projects"
widget   = "blank"
headless = true
active   = true
weight   = 35

[design.spacing]
  padding = ["60px", "0", "60px", "0"]

[advanced]
  css_class = "research-section"
+++

<div class="research-grid">

  <!-- LeakLess -->
  <a href="/publication/leakless/" class="rc">
    <div class="rc-top">
      <span class="rc-venue rv-blue">NDSS 2025</span>
      <span class="rc-tag">Serverless Security</span>
    </div>
    <h3 class="rc-title">LeakLess</h3>
    <p class="rc-desc">In-memory encryption protecting sensitive data against Spectre/Meltdown-class transient execution attacks in serverless platforms with minimal overhead.</p>
    <div class="rc-metrics">
      <div class="rc-metric"><strong>91%</strong><span>apps protected</span></div>
      <div class="rc-metric"><strong>2.8–8.5%</strong><span>overhead</span></div>
    </div>
    <div class="rc-footer">
      <span class="rc-link"><i class="fas fa-file-pdf"></i> Paper</span>
      <span class="rc-link"><i class="fab fa-github"></i> Code</span>
    </div>
  </a>

  <!-- KubeKeeper -->
  <a href="/publication/kubekeeper/" class="rc">
    <div class="rc-top">
      <span class="rc-venue rv-teal">IEEE EuroS&amp;P 2025</span>
      <span class="rc-tag">Kubernetes Security</span>
    </div>
    <h3 class="rc-title">KubeKeeper</h3>
    <p class="rc-desc">Cryptographic Secrets protection for Kubernetes using RBAC and Admission Webhooks, eliminating excessive-permission exposures with zero runtime overhead.</p>
    <div class="rc-metrics">
      <div class="rc-metric"><strong>498</strong><span>apps secured</span></div>
      <div class="rc-metric"><strong>0</strong><span>runtime overhead</span></div>
    </div>
    <div class="rc-footer">
      <span class="rc-link"><i class="fas fa-file-pdf"></i> Paper</span>
      <span class="rc-link"><i class="fab fa-github"></i> Code</span>
    </div>
  </a>

  <!-- LeakGauge -->
  <div class="rc">
    <div class="rc-top">
      <span class="rc-venue rv-orange">In Preparation</span>
      <span class="rc-tag">CI/CD Security</span>
    </div>
    <h3 class="rc-title">LeakGauge</h3>
    <p class="rc-desc">IaC-aware static analysis framework (CodeQL) tracing sensitive data flows across serverless deployments, designed as a CI/CD security guardrail.</p>
    <div class="rc-metrics">
      <div class="rc-metric"><strong>1,400+</strong><span>secrets found</span></div>
      <div class="rc-metric"><strong>500+</strong><span>apps analyzed</span></div>
    </div>
    <div class="rc-footer">
      <span class="rc-link rc-link-muted"><i class="fas fa-clock"></i> Coming Soon</span>
    </div>
  </div>

  <!-- Confine -->
  <a href="/publication/confine/" class="rc">
    <div class="rc-top">
      <span class="rc-venue rv-purple">Computers &amp; Security 2023</span>
      <span class="rc-tag">Container Security</span>
    </div>
    <h3 class="rc-title">Confine</h3>
    <p class="rc-desc">Automated seccomp policy generation for containers via static binary analysis, reducing attack surface by filtering unnecessary system calls.</p>
    <div class="rc-metrics">
      <div class="rc-metric"><strong>144+</strong><span>syscalls filtered</span></div>
      <div class="rc-metric"><strong>28</strong><span>CVEs mitigated</span></div>
    </div>
    <div class="rc-footer">
      <span class="rc-link"><i class="fas fa-file-pdf"></i> Paper</span>
      <span class="rc-link"><i class="fab fa-github"></i> Code</span>
    </div>
  </a>

</div>
