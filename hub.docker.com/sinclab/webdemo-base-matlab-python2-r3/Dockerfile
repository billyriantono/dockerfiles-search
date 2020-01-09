FROM ubuntu:14.04
MAINTAINER Milton Pividori <miltondp@gmail.com>

# Web Demo Builder - Base Docker image for MATLAB, Python 2.7.x and R 3.0.x

# Install base packages
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && apt-get install -y \
      libxt6 \
      libxmu6 \
      imagemagick \
      xorg \
      build-essential \
      pkg-config \
      gfortran \
      libatlas-base-dev \
      libatlas3gf-base \
      fonts-lyx \
      libfreetype6-dev \
      libpng-dev \
      python2.7 \
      python-dev \
      python-pip \
      python-tk \
      tk-dev \
      r-base \
      r-recommended \
      r-base-dev && \
    apt-get clean && apt-get autoclean


#
# MATLAB
#

COPY run_matlab.sh /


#
# Python 2.7.x
#

ENV python_env="/python_env"

RUN pip install -U virtualenv==12.0.7
RUN virtualenv ${python_env}

COPY install_python_module /usr/local/bin/
RUN install_python_module pip==6.0.8
RUN install_python_module numpy==1.9.2
RUN install_python_module scipy==0.15.1
RUN install_python_module scikit-learn==0.15.2
RUN install_python_module matplotlib==1.4.3
RUN install_python_module pandas==0.15.2
RUN install_python_module seaborn==0.5.1
RUN install_python_module sympy==0.7.6
RUN install_python_module biopython==1.65

RUN ln -s ${python_env}/bin/python /usr/local/bin/python

COPY matplotlibrc_tkagg /
COPY matplotlibrc_agg /


#
# R 3.0.x
#

ENV bioconductor_url="http://bioconductor.org/packages/2.12/bioc/src/contrib/"
ENV bioconductor_data_url="http://master.bioconductor.org/packages/2.12/data/annotation/src/contrib/"

COPY install.r /

RUN Rscript /install.r BiocInstaller 1.10.4 ${bioconductor_url}
RUN Rscript /install.r preprocessCore 1.22.0 ${bioconductor_url}
RUN Rscript /install.r BiocGenerics 0.6.0 ${bioconductor_url}
RUN Rscript /install.r Biobase 2.20.1 ${bioconductor_url}
RUN Rscript /install.r DBI 0.3.1
RUN Rscript /install.r RSQLite 1.0.0
RUN Rscript /install.r IRanges 1.18.4 ${bioconductor_url}
RUN Rscript /install.r AnnotationDbi 1.22.6 ${bioconductor_url}
RUN Rscript /install.r Rcpp 0.11.2
RUN Rscript /install.r RcppEigen 0.3.2.1.2
RUN Rscript /install.r minqa 1.2.3
RUN Rscript /install.r lme4 1.1-6
RUN Rscript /install.r profileModel 0.5-9
RUN Rscript /install.r brglm 0.5-8
RUN Rscript /install.r qvcalc 0.8-8
RUN Rscript /install.r relimp 1.0-3
RUN Rscript /install.r gnm 1.0-7
RUN Rscript /install.r gtools 3.4.1
RUN Rscript /install.r BradleyTerry2 1.0-4
RUN Rscript /install.r car 2.0-20
RUN Rscript /install.r plyr 1.8.1
RUN Rscript /install.r digest 0.6.4
RUN Rscript /install.r gtable 0.1.2
RUN Rscript /install.r stringr 0.6.2
RUN Rscript /install.r reshape2 1.4
RUN Rscript /install.r RColorBrewer 1.0-5
RUN Rscript /install.r dichromat 2.0-0
RUN Rscript /install.r colorspace 1.2-4
RUN Rscript /install.r munsell 0.4.2
RUN Rscript /install.r labeling 0.2
RUN Rscript /install.r scales 0.2.4
RUN Rscript /install.r proto 0.3-10
RUN Rscript /install.r ggplot2 1.0.0
RUN Rscript /install.r iterators 1.0.7
RUN Rscript /install.r foreach 1.4.2
RUN Rscript /install.r caret 6.0-30
RUN Rscript /install.r doParallel 1.0.8
RUN Rscript /install.r e1071 1.6-3
RUN Rscript /install.r gridExtra 0.9.1
RUN Rscript /install.r Matrix 1.1-3
RUN Rscript /install.r segmented 0.3-1.0
RUN Rscript /install.r mixtools 1.0.2


#
# Create a new user "developer".
# It will get access to the X11 session in the host computer
#

ENV uid=1000
ENV gid=${uid}

COPY init.sh /
COPY create_user.sh /

ENTRYPOINT ["/init.sh"]
CMD ["/create_user.sh"]

