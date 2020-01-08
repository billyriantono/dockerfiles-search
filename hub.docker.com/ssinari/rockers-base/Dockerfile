FROM rocker/r-ver:3.6.0
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    sudo \
    less \
    git \
    libssl-dev \
    libssh2-1-dev \
    libxml2-dev \
    zlib1g-dev \
    libcurl4-gnutls-dev \
    texlive-full \
    pandoc \
    pandoc-citeproc
    
ARG WHEN
SHELL ["/bin/bash", "-c"]
RUN R -e "install.packages( \
  c('devtools'     \
  , 'tidyverse'    \
  , 'Hmisc'        \
  , 'memisc'       \
  , 'ggplot2'      \
  , 'tables'       \
  , 'reshape2'     \
  , 'stargazer'    \
  , 'xtable'       \
  , 'rms'          \
  , 'lme4'         \
  , 'readxl'       \
  , 'RColorBrewer')\
  , repos = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')"

RUN R -e "if (!requireNamespace(\"BiocManager\", quietly = TRUE)) \
    install.packages(\"BiocManager\"); \
    BiocManager::install()"

CMD /bin/bash

