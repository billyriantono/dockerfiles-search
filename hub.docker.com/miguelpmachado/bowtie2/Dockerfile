FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="2.3.4.3-02"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y wget zip perl libtbb-dev python

RUN wget https://downloads.sourceforge.net/project/bowtie-bio/bowtie2/2.3.4.3/bowtie2-2.3.4.3-linux-x86_64.zip && \
    unzip bowtie2-2.3.4.3-linux-x86_64.zip && \
    rm bowtie2-2.3.4.3-linux-x86_64.zip

ENV PATH="/NGStools/bowtie2-2.3.4.3-linux-x86_64:${PATH}"

RUN apt-get remove -y wget zip && \
    apt-get autoclean -y

WORKDIR /data/
