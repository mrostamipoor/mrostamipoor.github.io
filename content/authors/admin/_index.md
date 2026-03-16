---
# Display name
title: Maryam Rostamipoor
summary: "Ph.D. candidate in Computer Science at Stony Brook University specializing in cloud, container, and application security — with over 10 years of research and industry experience."

# Username (this should match the folder name)
authors:
- admin

# Is this the primary user of the site?
superuser: true

# Role/position
role: Security Engineer | Security Researcher | PhD Candidate

# Organizations/Affiliations
organizations:
- name: Department of Computer Science, Stony Brook University
  url: "https://www.cs.stonybrook.edu/"

# Short bio (displayed in user profile at end of posts)
bio: Security Engineer and PhD researcher specializing in cloud security, Kubernetes hardening, secrets management, and penetration testing. Author of LeakLess (NDSS 2025), KubeKeeper (EuroS&P 2025), and Confine.

interests:
- Cloud & Platform Security
- Kubernetes & Container Security
- Secrets Management & Static Analysis
- Penetration Testing & Vulnerability Research
- CI/CD and IaC Security

tags:
- Kubernetes Security
- Cloud Computing
- Binary Analysis
- Application Security

education:
  courses:
  - course: Ph.D. in Computer Science
    institution: Stony Brook University
    year: 2026
  - course: M.S. in Computer Science
    institution: Stony Brook University
    year: 2023
  - course: M.E. in Information Security Engineering
    institution: Amirkabir University of Technology
    year: 2013
  - course: B.E. in Computer Engineering
    institution: Shiraz University of Technology
    year: 2011
# Social/Academic Networking
# For available icons, see: https://sourcethemes.com/academic/docs/page-builder/#icons
#   For an email link, use "fas" icon pack, "envelope" icon, and a link in the
#   form "mailto:your-email@example.com" or "#contact" for contact widget.
social:
- icon: envelope
  icon_pack: fas
  link: 'mailto:mrostamipoor@cs.stonybrook.edu'  # For a direct email link, use "mailto:test@example.org".
- icon: google-scholar
  icon_pack: ai
  link: https://scholar.google.com/citations?user=jUJfU5QAAAAJ&hl=en
- icon: github
  icon_pack: fab
  link: https://github.com/mrostamipoor
- icon: linkedin
  icon_pack: fab
  link: https://www.linkedin.com/in/maryam-rostamipoor/
- icon: twitter
  icon_pack: fab
  link: https://x.com/MRostamipoor
# Link to a PDF of your resume/CV from the About widget.
# To enable, copy your resume/CV to `static/files/cv.pdf` and uncomment the lines below.
- icon: cv
  icon_pack: ai
  link: files/MaryamRostamipoor-Resume-2026.pdf

# Enter email to display Gravatar (if Gravatar enabled in Config)
email: "mrostamipoor@cs.stonybrook.edu"

avatar:
  image: "avatar.jpg"   # place file at content/authors/admin/avatar.jpg
  shape: circle
# Organizational groups that you belong to (for People widget)
#   Set this to `[]` or comment out if you are not using People widget.
user_groups:
- Principal Investigators
---


I am a Security Engineer and Ph.D. candidate in Computer Science at Stony Brook University (graduating May 2026), advised by [Dr. Michalis Polychronakis](https://www3.cs.stonybrook.edu/~mikepo/). I have 8+ years of combined industry and research experience specializing in **cloud and platform security**, **Kubernetes and container hardening**, **secrets management**, **static analysis**, and **penetration testing**. I am a [Catacosinos Fellow](https://www.cs.stonybrook.edu/) (2025) and [NDSS Fellow](https://www.ndss-symposium.org/) (2025).

My research focuses on building production-grade security systems deployed across hundreds of real-world applications:

- **[LeakLess](https://github.com/mrostamipoor/LeakLess)** — In-memory encryption protecting sensitive data against memory-disclosure and transient-execution attacks (Spectre/Meltdown) in 91% of serverless applications with only 2.8–8.5% overhead. Published at **NDSS 2025**.
- **[KubeKeeper](https://github.com/mrostamipoor/KubeKeeper)** — Cryptographic Secrets protection for Kubernetes using RBAC and Admission Webhooks, eliminating excessive-permission exposures across 498 real-world applications with zero runtime overhead. Published at **EuroS&P 2025**.
- **LeakGauge** — IaC-aware static analysis framework (CodeQL) tracing sensitive data flows across serverless deployments, identifying 1,400+ secret-exposure paths across 500+ applications — designed as a CI/CD security guardrail.
- **[Confine](https://github.com/mrostamipoor/Confine)** — Automated seccomp policy generation for containers via static binary analysis, filtering 144+ system calls on average and mitigating 28 Linux kernel CVEs. Published in *Computers & Security*, 2023.

Prior to my Ph.D., I was **Head of Software Security** at Sadad Electronic Payment Company, leading threat modeling, security architecture reviews, and penetration testing across a national-scale banking ecosystem. I also performed offensive security assessments at APA Research Center and the Stock Exchange Organization, manually exploiting XSS, SQL injection, SSRF, IDOR, authentication bypass, and RCE vulnerabilities in production financial infrastructure.

I’m passionate about translating cutting-edge security research into practical defenses. Outside of research, I love cooking, yoga, working out, and spending time with friends.