FROM rocker/rstudio
MAINTAINER "Davide Albanese" <davide.albanese@gmail.com>

# Install latex for RStudio notebook (e.g. PDF output) end other packages
RUN apt-get update \
  && apt-get install -t unstable -y --no-install-recommends \
    libfftw3-dev \
    libtiff5-dev \
    texlive-latex-base

# Install packages for RStudio notebook
RUN install2.r --error \
    -r "https://cran.rstudio.com" \
    -r "http://www.bioconductor.org/packages/release/bioc" \
    bitops \
    caTools \
    digest \
    evaluate \
    formatR \
    highr \
    knitr \
    htmltools \
    markdown \
    rmarkdown \
    yaml

# Install required packages
RUN install2.r --error \
    -r "https://cran.rstudio.com" \
    -r "http://www.bioconductor.org/packages/release/bioc" \
    EBImage

# Install compmetagen packages
RUN install2.r --error \
    -r "https://cran.rstudio.com" \
    -r "http://www.bioconductor.org/packages/release/bioc" \
    corrplot \
    cowplot \
    dplyr \
    ggplot2 \
    ggtern \
    ggtree \
    gridExtra \
    phyloseq \
    plyr \
    psych \
    RColorBrewer \
    reshape2 \
    vegan

# Clean
RUN apt-get clean \
  && rm -rf /tmp/downloaded_packages/* \
  && rm -rf /var/lib/apt/lists/*
