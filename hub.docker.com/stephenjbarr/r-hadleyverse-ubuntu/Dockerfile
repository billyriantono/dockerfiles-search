FROM ubuntu:xenial-20180228

# Inspired by https://gist.github.com/pachamaltese/525ccd48a6cd4f577f59ba1088223483

RUN apt-get update && apt-get install -y \
    gdebi libxml2-dev libssl-dev libcurl4-openssl-dev libopenblas-dev r-base r-base-dev

RUN Rscript -e "install.packages(c('tidyverse','data.table','dtplyr','devtools','roxygen2','bit64'), repos = 'https://cran.rstudio.com/')"
