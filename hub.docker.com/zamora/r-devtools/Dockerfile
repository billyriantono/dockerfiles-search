## Adapted from rocker/r-devel, hadley/docker, and cardcorp/r-pandoc

# Use r-base + pandoc
FROM cardcorp/r-pandoc 

# Install external dependencies 
RUN apt-get update -qq \ 
  && apt-get install -t unstable -y --no-install-recommends \
    libcurl4-openssl-dev \
    libssl-dev \
    libsqlite3-dev \
    libxml2-dev \
    qpdf \
    vim \
    git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/ \
  && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# Install devtools and testthat
#RUN Rscript -e 'install.packages(c("devtools","testthat"),dependencies = TRUE)'
RUN install2.r --error \
  devtools \
  testthat
