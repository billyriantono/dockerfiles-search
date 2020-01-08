FROM rocker/tidyverse

#RUN echo 'utils::setRepositories(ind=1:4)' > ~/.Rprofile

COPY ./traj-converters /home/rstudio

#RUN /bin/bash -c 'git clone https://github.com/Stuartlab-UCSC/traj-converters.git'

RUN R -e 'install.packages(c("optparse","gam"));source("https://bioconductor.org/biocLite.R");biocLite("monocle")'
