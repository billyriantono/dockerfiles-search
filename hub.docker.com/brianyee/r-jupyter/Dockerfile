################## BASE IMAGE ######################

FROM brianyee/r-base

################## METADATA ######################

LABEL base_image="continuumio/miniconda:latest"
LABEL version="1"
LABEL software="R"
LABEL software.version="3.5.1"
LABEL about.summary="R-base with Jupyter and irkernel installed."
LABEL about.home="https://github.com/byee4/docker"
LABEL about.documentation=""
LABEL about.license_file=""
LABEL about.license=""
LABEL about.tags="Genomics"

################## MAINTAINER ######################
MAINTAINER Brian Yee <brian.alan.yee@gmail.com>

RUN apt-get update
RUN apt-get install -y apt-utils  build-essential gcc-multilib gfortran fort77
RUN apt-get install -y liblzma-dev libblas-dev libreadline-dev libbz2-dev libpcre3 libpcre3-dev libcurl4-openssl-dev libopenblas-base libssl-dev
RUN apt-get install -y default-jdk texlive-fonts-extra xorg-dev
RUN apt-get install -y libssh2-1-dev
RUN conda install -y -c r -c bioconda -c conda-forge \
    python=3.6 jupyter jupyterlab r=3.5.1 r-irkernel libjpeg-turbo=1.5 zeromq=4.2.5 readline=6.2
ENV PATH /opt/conda/bin:$PATH
RUN Rscript -e 'install.packages("devtools", repos="https://cran.rstudio.com")'
RUN Rscript -e 'remove.packages(c("curl","httr"))'
ENV CURL_CA_BUNDLE /opt/conda/lib/R/lib/microsoft-r-cacert.pem
RUN Rscript -e 'options("download.file.method" = "libcurl");devtools::install_github("IRkernel/IRkernel@1.0.2")'
RUN Rscript -e 'IRkernel::installspec(name = "R-3.5.1", displayname = "R-3.5.1", user = FALSE)'
