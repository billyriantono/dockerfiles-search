FROM ubuntu:14.04
MAINTAINER gaonkark@email.chop.edu

RUN apt-get update && apt-get install -y \
	autoconf \
	automake \
	wget \
	build-essential \
	tar \
	git \
	libreadline-gplv2-dev \
	libncursesw5-dev \
	libssl-dev \
	libsqlite3-dev \
	tk-dev \
	libgdbm-dev \
	libc6-dev \
	libbz2-dev

WORKDIR /opt

# Install python2.7
RUN cd /tmp && \
    wget https://www.python.org/ftp/python/2.7.9/Python-2.7.9.tgz && \
    tar xvfz Python-2.7.9.tgz && \
    cd Python-2.7.9 && \
    ./configure --prefix=/usr/local && \
    make && \
    make altinstall




RUN apt-get install -y python-pip
RUN apt-get install -y python-dev

RUN pip install pysam==0.9.0
RUN pip install PyPDF2==1.26.0
RUN pip install numpy==1.9.2
RUN apt-get install samtools
RUN apt-get update
RUN apt-get install -y r-base \
	r-base-dev

RUN echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" > ~/.Rprofile
RUN Rscript -e "install.packages('ggplot2')"
RUN Rscript -e "install.packages('reshape2')"
RUN Rscript -e "install.packages('gridExtra')"
RUN Rscript -e "install.packages('RColorBrewer')"
ENV PATH="/usr/local/lib/python2.7/dist-packages:${PATH}"

WORKDIR /opt
RUN pip install telomerehunter==1.1.0

