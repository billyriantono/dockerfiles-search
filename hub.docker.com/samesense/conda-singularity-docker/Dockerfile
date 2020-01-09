FROM continuumio/miniconda3
MAINTAINER Perry Evans <https://github.com/samesense>

RUN apt-get update -qqq \
&& apt-get install -y wget curl git squashfs-tools build-essential libtool autotools-dev automake autoconf python

RUN wget https://github.com/singularityware/singularity/releases/download/2.4.6/singularity-2.4.6.tar.gz
RUN tar xvzf singularity-2.4.6.tar.gz \
&& cd singularity-2.4.6 \
&& ./configure \
&& make \
&& make install

RUN cd ..

RUN apt-get autoremove -y \
&& apt-get remove --purge -y git

RUN rm -rf singularity-2.4.6
