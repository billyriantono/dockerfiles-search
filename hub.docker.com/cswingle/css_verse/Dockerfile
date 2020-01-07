FROM rocker/verse

MAINTAINER Christopher Swingley <cswingle@swingleydev.com>

ADD /rstudio_monitored_user-settings_user-settings /home/rstudio/.rstudio/monitored/user-settings/user-settings

RUN apt-get update -qq && apt-get -y --no-install-recommends install \
  libgdal-dev \
  libproj-dev \
  libgeos-dev \
  libprotobuf-dev \
  protobuf-compiler \
  libjq-dev \
  libudunits2-dev \
  vim-nox \
  dc \
  && R -e "source('https://bioconductor.org/biocLite.R')" \
  && install2.r --error \
      --deps TRUE \
      RPostgreSQL \
      dbplyr \
      pool \
      rgdal \
      sp \
      sf \
      leaflet \
      maptools \
      lubridate \
      randomForest \
      jsonlite \
      rvest \
      spatial \
      svglite
