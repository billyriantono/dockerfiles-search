FROM rocker/verse:3.6.1

RUN apt-get update -qq \
  && R -e "install.packages('qtl2', repos='https://rqtl.org/qtl2cran')"

