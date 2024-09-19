---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Confine: Fine-grained System Call Filtering for Container Attack Surface Reduction"
authors: ["admin", "Seyedhamed Ghavamnia", "Michalis Polychronakis"]
date: 2023-09-01
#doi: "10.1214/20-AOAS1401"

# Schedule page publish date (NOT publication's date).
#publishDate: 2020-06-13T21:28:45Z

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "In Computers & Security, vol. 132, September 2023"
publication_short: ""

abstract: "Confine uses static code analysis to inspect the containerized application and all its dependencies, identify the superset of system calls required for the correct operation of the container, and generate both a container-wide and application-specific Seccomp system call policy that can be readily enforced while loading the container and launching the main program. We also show that further attack surface reduction is possible by enforcing fine-grained system call policies that do not only consider the system calls used by the target application, but also their argument values.
The results of our experimental evaluation with a set of 27 Docker images show that applying container-wide filtering disables more than 145 system calls on average across the entire container, and application-specific filtering increases the number of filtered system calls by 25% on average, as many system calls used exclusively by utilities and scripts during the container’s initialization phase can be safely removed afterwards."

# Summary. An optional shortened abstract.
summary: ""

tags: ["Debloating", "Attack Surface Reduction", "Program Analysis", "System Call Filtering", "Argument oncretization"]
categories: []
#featured: true

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: files/confine.pdf
url_code: https://github.com/mrostamipoor/confine
url_dataset: https://github.com/mrostamipoor/confine/blob/master/images.json
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
projects: ["confine"]

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---
