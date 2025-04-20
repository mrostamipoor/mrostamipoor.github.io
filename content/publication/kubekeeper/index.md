---


title: "KubeKeeper: Protecting Kubernetes Secrets Against Excessive Permissions"
authors: ["admin", "Aliakbar Sadeghi", "Michalis Polychronakis"]
date: 2025-06-01

publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "In Proceedings of the 10th IEEE European Symposium on Security and Privacy (EuroS&P). Venice, Italy."
publication_short: ""

abstract: "KubeKeeper is a comprehensive solution for protecting Kubernetes Secrets against leakage due to excessive permissions. KubeKeeper automatically encrypts Secrets and ensures that only explicitly authorized Pods can access their decrypted form. This is achieved by integrating with Kubernetes’ admission control framework to transparently enforce access policies, without requiring changes to application code and with minimal integration effort into existing cluster infrastructure. We evaluated KubeKeeper on a diverse set of 498 Kubernetes applications and demonstrate that it successfully protects Secrets against all identified excessive permissions, without introducing performance degradation during execution or any significant overhead during Pod creation and deployment."

# Summary. An optional shortened abstract.
summary: ""

tags: ["Cloud Computing", "Kubernetes", "Excessive Permissions", "Secrets Management"]
categories: []
featured: true

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: files/kubekeeper.pdf
url_code: https://github.com/mrostamipoor/KubeKeeper
#url_dataset: https://github.com/mrostamipoor/LeakLess/tree/main/leakless-dataset
url_poster:
url_project:
url_slides: 
url_source:
url_video: 

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
#projects: ["leakless"]

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---
