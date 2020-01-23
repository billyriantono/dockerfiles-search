FROM rocker/r-ver:latest

LABEL maintainer="Harm Verschuren"
LABEL organisation="EDSN Data-analytics"

RUN apt-get update -qq && \
    apt-get -y --no-install-recommends install \
    libxml2-dev \
    libcairo2-dev \
    unixodbc-dev \
    libsqlite3-dev \
    libpq-dev \
    libssh2-1-dev \
    libssl-dev \
    libcurl4-openssl-dev

RUN install2.r --error --deps TRUE --repos http://cran.rstudio.com \
    DataExplorer \
    devtools \
    forecast \
    ggpubr \
    gridExtra \
    png \
    roxygen2 \
    tidyverse

COPY .Rprofile /home
