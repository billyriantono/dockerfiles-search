FROM crukcibioinformatics/bss-introbioc
MAINTAINER Mark Fernandes<mark.fernandes@cruk.cam.ac.uk>
# Prognostic Signatures session
#------------------------------
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update 
RUN apt-get install --fix-missing -y git
RUN mkdir -p /home/participant/
# RUN git clone --recursive https://github.com/bioinformatics-core-shared-training/cruk-autumn-school-2017.git /home/participant/Course_Materials

# Install R packages for different sections
COPY Prognosticsig/install_prog.R /home/participant/Course_Materials/

RUN R -f /home/participant/Course_Materials/install_prog.R

# RUN rm -rf /tmp
RUN chown rstudio /home/participant/Course_Materials/
WORKDIR /home//participant/Course_Materials/
