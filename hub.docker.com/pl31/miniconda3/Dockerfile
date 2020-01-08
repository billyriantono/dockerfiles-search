FROM pl31/debian:jessie
MAINTAINER Patrick Büch <dh@paco.pl31.de>

# install services
RUN echo "Europe/Berlin" > /etc/timezone && \
    dpkg-reconfigure tzdata && \
    apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y install \
        wget bzip2 && \
    (cd ~ && wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh) && \
    chmod +x ~/Miniconda3-latest-Linux-x86_64.sh && \
    ~/Miniconda3-latest-Linux-x86_64.sh -b && \ 
    rm ~/Miniconda3-latest-Linux-x86_64.sh

ENV PATH $PATH:/root/miniconda3/bin
