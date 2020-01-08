FROM rocker/r-ver:3.6.0

## dependencies for R packages
RUN apt-get update && \
	apt-get -y install wget libpq-dev libxml2-dev libcurl4-openssl-dev libssl-dev libz-dev

## install R packages
RUN R -e "install.packages(c('tidyverse', 'dbplyr', 'lubridate', 'DBI', 'RPostgres', 'jsonlite', 'logger', 'config'))"

VOLUME /scripts
WORKDIR /scripts

ENTRYPOINT [ "/usr/local/bin/Rscript" ]