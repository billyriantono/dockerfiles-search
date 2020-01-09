# Use rocker/r-ver as the base image
# This will inherit everyhing that was installed into base image already
# Documented at https://hub.docker.com/r/rocker/r-ver/~/dockerfile/
FROM rocker/r-ver:3.4.4

# Install any dependencies required for the R packages
RUN apt-get update   \
    && apt-get install -y --no-install-recommends   libxml2-dev   libcurl4-openssl-dev   libssl-dev   libv8-3.14-dev

# Install lavaan dependencies
RUN apt-get install -y gfortran

RUN apt-get update   \
    && apt-get -y upgrade

# Install the R Packages from CRAN
RUN Rscript -e 'source("https://bioconductor.org/biocLite.R"); biocLite(c("RBGL", "graph"))'
RUN Rscript -e 'install.packages(c("pcalg", "CAM", "bnlearn"))'

# Configure file path
RUN mkdir /root/my-project
VOLUME /root/my-project
WORKDIR /root/my-project

# GPArotation
RUN Rscript -e 'packageurl <- "https://cran.r-project.org/src/contrib/GPArotation_2014.11-1.tar.gz"; install.packages(packageurl, repos=NULL, type="source")'

# lavaan
RUN Rscript -e 'install.packages(c("mnormt", "pbivnorm", "numDeriv")); packageurl <- "https://cran.r-project.org/src/contrib/lavaan_0.6-3.tar.gz"; install.packages(packageurl, repos=NULL, type="source")'


# semTools
RUN Rscript -e 'packageurl <- "https://cran.r-project.org/src/contrib/semTools_0.5-1.tar.gz"; install.packages(packageurl, repos=NULL, type="source")'

CMD tail -f /dev/null