FROM rocker/tidyverse:latest

RUN apt-get install -y libgsl-dev
RUN R -e "source('https://bioconductor.org/biocLite.R');biocLite();biocLite(c('GenomicFeatures', 'DESeq2', 'Rsamtools', 'AnnotationDbi','GenomicAlignments', 'BiocParallel','tximport', 'devtools', 'remotes', 'GenomeInfoDbData'))" 
