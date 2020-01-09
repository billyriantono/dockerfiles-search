FROM ubuntu:16.04
MAINTAINER felix11h.dev@gmail.com

USER root

RUN apt-get update
RUN apt-get install -y git python3-pip python3-nose screen
RUN pip3 install ipython numpy scipy matplotlib pandas gitpython sumatra 

# Adapted from Ivo Jimenez
RUN apt-get -yq update && \
    apt-get install -qy --fix-missing \
        texlive \
        texlive-latex-extra \
	texlive-science \
        texlive-math-extra \
	dvipng && \
    apt-get -yq autoremove && \
    apt-get clean -y && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN useradd -ms /bin/bash docker

WORKDIR /home/lab
