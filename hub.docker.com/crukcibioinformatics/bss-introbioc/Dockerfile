FROM rocker/rstudio
MAINTAINER Mark Fernandes<mark.fernandes@cruk.cam.ac.uk>
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update 
RUN apt-get install --fix-missing -y git
RUN mkdir -p /home/participant/
RUN git clone --recursive https://github.com/bioinformatics-core-shared-training/cruk-summer-school-2019.git /home/participant/Course_Materials

# Set Rstudio password
ENV PASSWORD=summerschool

RUN chown rstudio /home/participant/Course_Materials/ /tmp
WORKDIR /home/participant/Course_Materials/
