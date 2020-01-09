FROM keyeoh/totoro_metharray

MAINTAINER Gustavo F. Bayon <fernandezgustavo@uniovi.es>

RUN apt-get install -y openjdk-7-jdk openjdk-7-jre  

RUN Rscript -e "source('http://bioconductor.org/biocLite.R')" \
  -e "biocLite('topGO', ask = FALSE)" \
  -e "biocLite('xlsx', ask = FALSE)"

RUN curl http://download.r-forge.r-project.org/src/contrib/Vennerable_3.0.tar.gz\
  > Vennerable_3.0.tar.gz && \
  R CMD INSTALL Vennerable_3.0.tar.gz
