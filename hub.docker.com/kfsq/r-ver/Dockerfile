FROM rocker/r-ver:3.4.3

LABEL org.label-schema.license="GPL-2.0,MPL-2.0" \
      org.label-schema.vcs-url="https://github.com/kfsq/gitlab-ci-docker" \
      org.label-schema.vendor="Docker images for use with GitLab CI" \
      maintainer="Kristoffer Winther Balling <kfsq@novonordisk.com>"

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  ## Debian packages for SSL
  libssl-dev \
  libcurl4-openssl-dev \
  ## Debian packages for GIS
  libgdal-dev \
  libgeos-dev \
  libudunits2-dev \
  ## Debian packages for V8
  libv8-3.14-dev \
  libprotobuf-dev \
  libjq-dev \
  protobuf-compiler \
  # Debian packages Java (for rJava)
  libbz2-dev \
  openjdk-8-jdk \
  # Debian packages pandoc (for rmarkdown/knitr)
  pandoc \
  # Debian packages for gdtools/tmap/mapview
  libcairo2-dev \
  ## Xaringan and decktape
  curl \
  libpython2.7 \
  libx11-xcb1 \
  libxcomposite-dev \
  libxcursor-dev \
  libxdamage-dev \
  libxtst-dev \
  libnss3 \
  chromium \ 
  libgconf-2-4 \
  gnupg2 \
  && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
  && apt-get install -y nodejs \
  && npm install decktape \
  # Configure Java for R (for rJava)
  && R CMD javareconf \
  ## Install R packages
  && Rscript -e "install.packages(c( \
  'import', \
  'ggplot2', \
  'knitr', \
  'magrittr', \
  'stringi', \
  'xml2', \
  'shiny', \
  'shinydashboard', \
  'dygraphs', \
  'plotly', \
  'shinyWidgets', \
  'data.table', \
  'stringi', \
  'lubridate', \
  'rhandsontable', \
  'leaflet', \
  'matrixStats', \
  'sp', \
  'whisker', \
  'digest', \
  'RJDBC', \
  'htmlwidgets', \
  'testthat', \
  'plyr', \
  'dplyr', \
  'rmarkdown', \
  'assertive', \
  'ISOweek', \
  'choroplethr', \
  'choroplethrMaps', \
  'rgeos', \
  'rgdal', \
  'maptools', \
  'leaflet', \
  'scales', \
  'mapview', \
  'tmap', \
  'tmaptools', \
  'rmapshaper', \
  'shinycssloaders', \
  'rprojroot', \
  'xaringan', \
  'reticulate' \
  ))" \
  ## Clean up
  && cd / \
  && rm -rf /tmp/* \
  && apt-get autoremove -y \
  && apt-get autoclean -y \
  && rm -rf /var/lib/apt/lists/*
