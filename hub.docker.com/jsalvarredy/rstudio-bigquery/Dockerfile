FROM rocker/rstudio

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    zlib1g-dev

RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('bigrquery')"
RUN Rscript -e "library('devtools')"
RUN Rscript -e "library('bigrquery')"
RUN Rscript -e "devtools::install_github('rstats-db/bigrquery', force=TRUE)"
