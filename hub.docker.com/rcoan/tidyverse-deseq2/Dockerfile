FROM rocker/tidyverse:3.4.4

LABEL maintainer="Rafael Coan (rafael.coan@unesp.br)" \
      date="07/06/2018" \
      description="A rstudio version with DESeq2."

RUN R -e "source('https://bioconductor.org/biocLite.R'); biocLite(c('rjson', 'GenomicFeatures', 'ensembldb', 'org.Hs.eg.db', 'pheatmap','IHW','vsn','tximport','DESeq2'))"
