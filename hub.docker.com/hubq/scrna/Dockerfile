FROM rocker/rstudio-stable:devel

RUN echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" > ~/.Rprofile
RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e 'library(devtools);install_github("satijalab/seurat")'
RUN Rscript -e 'install.packages("data.table")'

RUN apt-get update
RUN apt-get -y install openjdk-7-jre  openjdk-7-jdk
