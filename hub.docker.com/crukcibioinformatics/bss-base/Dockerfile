FROM rocker/rstudio
MAINTAINER Mark Fernandes<mark.fernandes@cruk.cam.ac.uk>
# Install git and clear up after it
RUN apt-get update && apt-get install --fix-missing -y git && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /home/participant/Course_Materials
# RUN git clone --recursive https://github.com/bioinformatics-core-shared-training/cruk-summer-school-2019.git /home/participant/Course_Materials

# Set Rstudio password
ENV PASSWORD=summerschool

RUN chown rstudio /home/participant/Course_Materials/ /tmp
WORKDIR /home/participant/Course_Materials/
