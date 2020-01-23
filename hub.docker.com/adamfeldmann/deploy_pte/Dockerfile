FROM rocker/verse:latest

MAINTAINER  Adam Feldmann and Robert Herczeg  <adam.feldmann@aok.pte.hu>
# Version handling , newest Apache Spark, sparklyR package to access Spark from R, dplyr R package 
ENV SPARK_VERSION 2.3.0
ENV SPARKLYR_VERSION 0.7.0
ENV DPLYR_VERSION 0.7.4
# reliable source
RUN echo 'options(repos = c(CRAN = "https://cran.rstudio.com"))' > .Rprofile
# Install Apaches spark from R using sparklyr package
Run R -e 'devtools::install_version("dplyr", version = Sys.getenv("DPLYR_VERSION"))'
RUN R -e 'devtools::install_github("rstudio/sparklyr")'
RUN R -e 'str_spark_version = Sys.getenv("SPARK_VERSION"); sparklyr::spark_install(str_spark_version)'
RUN echo 'rsession-which-r=/usr/local/bin/R' > /etc/rstudio/rserver.conf
RUN mkdir /home/rstudio/.cache
RUN mv /root/spark/ /home/rstudio/.cache
RUN chown -R rstudio:rstudio /home/rstudio/.cache
RUN mkdir /root/main
ENV RSTUDIO_SPARK_HOME /home/rstudio/.cache/spark/spark-2.3.0-bin-hadoop2.7


