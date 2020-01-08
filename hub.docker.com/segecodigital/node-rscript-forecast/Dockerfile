FROM node:10

# install R
RUN echo 'deb http://cran.r-project.org/bin/linux/debian stretch-cran35/' >> /etc/apt/sources.list
RUN apt-get update
RUN apt install r-base -y --allow-unauthenticated

# install forecast library
COPY install.R /home/install.R
RUN Rscript /home/install.R
