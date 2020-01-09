FROM rocker/tidyverse:latest

RUN apt-get update -qq && apt-get -y --no-install-recommends install \
  libtiff5-dev \
  libxt-dev \
  && install2.r --error \
    --deps TRUE \
    foreach \
    doParallel \
    reticulate \
    RSelenium \
    imager \
    selectr
