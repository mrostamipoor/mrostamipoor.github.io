---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "LeakLess: Selective Data Protection Against Memory Leakage Attacks for Serverless Platforms"
authors: ["admin", "Seyedhamed Ghavamnia", "Michalis Polychronakis"]
date: 2025-02-28
#doi: "10.1214/20-AOAS1401"

# Schedule page publish date (NOT publication's date).
#publishDate: 2020-06-13T21:28:45Z

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "In Proceedings of the Network and Distributed System Security Symposium (NDSS). San Diego, CA"
publication_short: ""

abstract: "LeakLess is an approach for protecting secret data against memory disclosure vulnerabilities and transient execution attacks on serverless computing platforms that use language-level sandboxing to run untrusted code. LeakLess relies on selective in-memory encryption of developer-annotated sensitive data and addresses the limitations of previous selective data protection techniques by combining in-memory encryption with a separate I/O module. This enables the safe transmission of protected data between serverless functions and external hosts. We implemented LeakLess on the Spin serverless platform and evaluated it with real-world serverless applications. Our results demonstrate that LeakLess provides robust protection while incurring only a minor throughput decrease—up to 2.8% when the I/O module runs on a different host than the Spin runtime, and up to 8.5% when it runs on the same host."

# Summary. An optional shortened abstract.
summary: ""

tags: ["Serverless Platforms", "Selective Data Protection", "Transient Execution Attacks", "Memory Disclosure"]
categories: []
featured: true

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: files/leakless.pdf
url_code: https://github.com/mrostamipoor/LeakLess
url_dataset: https://github.com/mrostamipoor/LeakLess/tree/main/leakless-dataset
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
