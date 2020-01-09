# docker build --rm -t r-iscte .
FROM lipcomputing/rbase

RUN apt-get -y install r-cran-rmpi
ADD installpackages.R /home/installpackages.R
RUN R CMD BATCH /home/installpackages.R

