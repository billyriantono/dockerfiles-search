FROM bioconductor/release_base2:R3.6.0_Bioc3.9

RUN touch /var/lib/dpkg/available
RUN apt-get update && \
    apt-get install -y --fix-missing build-essential zlib1g-dev unzip libncurses5-dev curl wget python python-pip python-dev cmake libboost-all-dev  libxml2-dev libcurl4-gnutls-dev software-properties-common apt-transport-https default-jre default-jdk less vim libtbb-dev git

# RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
# RUN add-apt-repository 'deb [arch=amd64,i386] https://cran.rstudio.com/bin/linux/ubuntu xenial/'
# RUN apt-get update
# RUN apt-get install -y r-base-core r-recommended r-base-dev r-doc-html
# RUN apt-get install -y --fix-missing r-base=${R_VERSION}-1bionic  r-recommended=${R_VERSION}-1bionic 
# RUN apt-get install -y --fix-missing --allow-downgrades r-base-core=${R_VERSION}-1bionic

# RUN echo 'local({r <- getOption("repos"); r["CRAN"] <- "http://cran.r-project.org"; options(repos=r)})' > ~/.Rprofile
# RUN R -e 'source("http://bioconductor.org/biocLite.R"); biocLite("DESeq2"); biocLite("tximport"); biocLite("readr");'
RUN R -e 'BiocManager::install(c("ConsensusClusterPlus","DESeq2","tximport","readr","shiny"))'
