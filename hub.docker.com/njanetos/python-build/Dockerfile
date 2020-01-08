# GPLv3
FROM njanetos/texlive:latest
MAINTAINER njanetos <nejanetos@gmail.com>
LABEL Description="Python build environment"

RUN rm -rf /var/lib/apt/lists/* && \
    apt-get update && \
    apt-get install -y python3 python3-pip make r-base && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install matplotlib

RUN pip3 install numpy

RUN pip3 install scipy

RUN pip3 install pandas

RUN pip3 install statsmodels

RUN pip3 install seaborn
