FROM rocker/rstudio
MAINTAINER "Deni Ribicic" <dribicic@gmail.com>

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    libfftw3-dev \
    libtiff5-dev \
    texlive-latex-base


#install cran-R and bioconductor packages
RUN install2.r --error \
    -r "https://cran.rstudio.com" \
    -r "http://www.bioconductor.org/packages/release/bioc" \
    phyloseq \
    reshape2 \
    vegan
    
# Clean
RUN apt-get clean \
  && rm -rf /tmp/downloaded_packages/* \
  && rm -rf /var/lib/apt/lists/*
