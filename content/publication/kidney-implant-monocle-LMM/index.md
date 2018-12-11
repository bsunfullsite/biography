+++
title = "Transcriptional trajectories of human kidney injury progression"
date = 2018-11-01T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Bo Sun(co-first)","Pietro E. Cippà(co-first)", "Jing Liu", 
"Liang Chen", "Maarten Naesens","Andrew P. McMahon"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["2"]

# Publication name and optional abbreviated version.
publication = "In *JCI insight*"
#publication_short = "In *JCI insight*"

# Abstract and optional shortened version.
abstract = "We investigated a complex clinical condition applying an unsupervised computational strategy, which integrates genome-wide expression analysis in heterogeneous groups of patients to identify and characterize shared trajectories of disease progression. The integration of multiple transcriptomes from serial biopsies with advanced computational algorithms overcame the analytical hurdles related to variability between individuals and identified shared transcriptional elements of kidney disease progression in humans, which may prove as useful predictors of disease progression following kidney transplantation and kidney injury. This generally applicable approach opens the way for an unbiased analysis of human disease progression."


# Is this a selected publication? (true/false)
selected = true

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects = ["research"]

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["R", "research", "Shiny"]

# Links (optional).
url_pdf = "https://insight.jci.org/articles/view/123151/pdf"
url_preprint = "https://insight.jci.org/articles/view/123151?utm_source=TrendMD&utm_medium=cpc&utm_campaign=JCI_Insight_TrendMD_0"
url_GeneViz = "https://lianglabusc.shinyapps.io/shinyapp/"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
url_custom = [{name = "GENEVIZ1.0", url = "https://lianglabusc.shinyapps.io/shinyapp/"}]

# Digital Object Identifier (DOI)
doi = "https://doi.org/10.1172/jci.insight.123151"

# Does this page contain LaTeX math? (true/false)
math = true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = "Figure 2 from the paper"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Center"
+++

**Highlight**  

In this research, I applied a Linear Mixed Model to achieve variance decomposition, which is pretty interesting. It helps us distinguish between genes that are explained more by confounding variables like *sex*, *immune reponse*, from the real signals that are explained by *injury stage*. 
