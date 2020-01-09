FROM ubuntu:18.04
LABEL author="Mohamed Alibi" \
description="Docker image for Genetic Analysis of Population-based Association Studies (23rd to 27th September)" \
maintainer="Mohamed Alibi <alibi@ebi.ac.uk>"

# Pre requirements
########
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_GB.UTF-8
ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get install -y --reinstall language-pack-en \
    && apt-get install -y gnupg gdebi expect \
    && locale-gen en_GB.UTF-8

RUN echo "deb http://cloud.r-project.org/bin/linux/ubuntu bionic/" >> /etc/apt/sources.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update; apt-get install -y \
        build-essential cmake curl ghostscript git gnuplot groff help2man lsb-release python python-pip r-base rpm \
        zlib1g-dev libbz2-dev libncurses5-dev libncursesw5-dev liblzma-dev gcc make libcurl4-openssl-dev build-essential \
        ca-certificates automake pkg-config sudo wget git autoconf zlibc nano libedit2 libssl-dev libgsl-dev \
        r-base r-base-core r-recommended \
        && pip install cget

# Set default CRAN repo
########
#COPY ./installer.R /usr/local/installer.R
#RUN Rscript /usr/local/installer.R
RUN echo 'options(repos = c(CRAN = "https://cran.rstudio.com/"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
    && echo 'source("/etc/R/Rprofile.site")' >> /etc/littler.r \
    && ln -s /usr/share/doc/littler/examples/install.r /usr/local/bin/install.r \
    && ln -s /usr/share/doc/littler/examples/install2.r /usr/local/bin/install2.r \
    && ln -s /usr/share/doc/littler/examples/installGithub.r /usr/local/bin/installGithub.r \
    && ln -s /usr/share/doc/littler/examples/testInstalled.r /usr/local/bin/testInstalled.r \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
    && echo '"\e[5~": history-search-backward' >> /etc/inputrc \
    && echo '"\e[6~": history-search-backward' >> /etc/inputrc \
    && chmod 777 -R /usr/local/lib/R/ \
    && chmod 777 -R /usr/lib/R/ \
    && chmod 777 -R /usr/share/R/

# Install htslib
########
ADD https://github.com/samtools/htslib/releases/download/1.9/htslib-1.9.tar.bz2 /usr/local/htslib.tar.bz2
RUN tar xvjf /usr/local/htslib.tar.bz2 -C /usr/local/ \
    && chmod 777 -R /usr/local/htslib-1.9 \
    && cd /usr/local/htslib-1.9 \
    && ./configure \
    && make \
    && make install \
    && rm /usr/local/htslib.tar.bz2

ADD https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2 /usr/local/bcftools.tar.bz2
RUN tar xvjf /usr/local/bcftools.tar.bz2 -C /usr/local/ \
    && chmod 777 -R /usr/local/bcftools-1.9 \
    && cd /usr/local/bcftools-1.9 \
    && ./configure \
    && make \
    && make install \
    && rm /usr/local/bcftools.tar.bz2

## Install EPACTS
########

WORKDIR /usr/local/EPACTS
COPY . /usr/local/EPACTS
RUN cget install -DCMAKE_C_FLAGS="-fPIC" -DCMAKE_CXX_FLAGS="-fPIC" -f requirements.txt \
    && mkdir -p /usr/local/EPACTS/build

WORKDIR /usr/local/EPACTS/build
RUN cmake -DCMAKE_TOOLCHAIN_FILE=../cget/cget/cget.cmake -DCMAKE_BUILD_TYPE=Release .. \
    && make \
    && make install \
    && rm -rf /usr/local/EPACTS

## Create user training
########
RUN useradd -r -s /bin/bash -U -m -d /home/training -p '' training

# Setup the user environment
########
ENV HOME /home/training
RUN usermod -aG sudo,audio,video training \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
    && mkdir /home/training/DATA \
    && chown -R training:training /home/training/DATA \
    && chmod 777 -R /home/training/DATA

WORKDIR $HOME
USER training
