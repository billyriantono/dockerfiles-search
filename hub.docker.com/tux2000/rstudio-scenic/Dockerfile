# Based on the rocker rstudio image
# https://github.com/rocker-org/rocker-versioned/tree/master/rstudio
FROM rocker/rstudio:latest

# Install needed packages in Debian
RUN apt-get update --yes && apt-get install --no-install-recommends --yes \
  libxml2-dev \
  zlib1g-dev \
  libssh2-1-dev

# Install R dependencies for Scenic
# based on https://htmlpreview.github.io/?https://github.com/aertslab/SCENIC/blob/master/vignettes/SCENIC_Intro.html
RUN \
  R -e 'install.packages(c("devtools", "Rcpp","RcppArmadillo","knitr","rmarkdown"), repos="https://ftp.acc.umu.se/mirror/CRAN/")'

RUN \
    R -e 'source("https://bioconductor.org/biocLite.R"); biocLite(c("GENIE3", "RcisTarget", "AUCell","mixtools","NMF", "Rtsne", "R2HTML","doMC", "doRNG","SingleCellExperiment"), suppressAutoUpdate=TRUE, ask=FALSE, suppressUpdates=TRUE)'

# Install SCENIC
RUN \
    R -e 'devtools::install_github("aertslab/SCENIC")'

# Download reference DBs for human and mouse
RUN \
    R -e 'dir.create("/home/rstudio/cisTarget_databases"); setwd("/home/rstudio/cisTarget_databases");      dbFilesHs <- c("https://resources.aertslab.org/cistarget/databases/homo_sapiens/hg19/refseq_r45/mc9nr/gene_based/hg19-500bp-upstream-7species.mc9nr.feather","https://resources.aertslab.org/cistarget/databases/homo_sapiens/hg19/refseq_r45/mc9nr/gene_based/hg19-tss-centered-10kb-7species.mc9nr.feather");      dbFilesMm <- c("https://resources.aertslab.org/cistarget/databases/mus_musculus/mm9/refseq_r45/mc9nr/gene_based/mm9-500bp-upstream-7species.mc9nr.feather","https://resources.aertslab.org/cistarget/databases/mus_musculus/mm9/refseq_r45/mc9nr/gene_based/mm9-tss-centered-10kb-7species.mc9nr.feather");      for(featherURL in c(dbFilesHs,dbFilesMm)){download.file(featherURL, destfile=basename(featherURL));descrURL <- gsub(".feather$", ".descr", featherURL);if(file.exists(descrURL)) download.file(descrURL, destfile=basename(descrURL))}'

# More packages needed for example
RUN \
  R -e 'source("https://bioconductor.org/biocLite.R"); biocLite(c("GEOquery"), suppressAutoUpdate=TRUE, ask=FALSE, suppressUpdates=TRUE)'
RUN \
  R -e 'install.packages(c("data.table","zoo","rbokeh","rsconnect","Cairo"), repos="https://ftp.acc.umu.se/mirror/CRAN/")'
