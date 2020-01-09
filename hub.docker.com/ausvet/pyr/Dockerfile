FROM rocker/tidyverse:3.5

COPY ./installpackages.r /
RUN Rscript /installpackages.r

# Setup source for python 3.6
RUN echo "deb http://deb.debian.org/debian testing main" >> /etc/apt/sources.list  && \
    echo 'APT::Default-Release "stable";' | sudo tee -a /etc/apt/apt.conf.d/00local


RUN apt-get update && \
    apt-get -y install \
        libreadline-dev \
        liblapack-dev

# install from testing
RUN apt-get -y -t testing install \
        python3 \
        python3-pip \
        python3-gdal \
        python3-rpy2

# RUN python3 --version

# create /etc/***/libR.conf
RUN echo "/usr/local/lib/R/lib/" > /etc/ld.so.conf.d/libR.conf
RUN ldconfig

RUN pip3 install -U \
        rpy2 \
        pytz \
        pandas \
        tzlocal

# RUN python3 -m 'rpy2.tests'

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

CMD './docker_start.sh'
