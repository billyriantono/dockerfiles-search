FROM crukcibioinformatics/bss-introbioc
MAINTAINER Mark Fernandes<mark.fernandes@cruk.cam.ac.uk>
RUN rm -rf /var/lib/apt/lists/*
# add contrib and non-free sources
COPY etc_apt_sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install --fix-missing -y git apt-utils python-pip findutils python-dev libxml2-dev ghostscript libexpat1-dev libgit2-dev zlib1g-dev 
RUN mkdir -p /home/participant/
#
#RUN git clone --recursive https://github.com/bioinformatics-core-shared-training/cruk-summer-school-2019.git /home/participant/Course_Materials
#
# Install cutadapt and macs2
COPY ChIPSeq/install_chip.sh /home/participant/Course_Materials/
RUN chmod +x /home/participant/Course_Materials/install_chip.sh
RUN /home/participant/Course_Materials/install_chip.sh

# Install R packages 
COPY ChIPSeq/install_chip.R /home/participant/Course_Materials/
RUN R -f /home/participant/Course_Materials/install_chip.R && rm -rf /tmp
RUN chown rstudio /home/participant/Course_Materials/
WORKDIR /home//participant/Course_Materials/
