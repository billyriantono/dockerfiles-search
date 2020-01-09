FROM ubuntu:14.04

MAINTAINER Christian Brenninkmeijer <Christian.Brenninkmeijer@manchester.ac.uk>

# See https://cran.r-project.org/bin/linux/ubuntu/README
RUN echo "deb http://mirrors.ebi.ac.uk/CRAN/bin/linux/ubuntu trusty/" >> /etc/apt/sources.list

#Install curl, R, and R packages
RUN apt-get update  && apt-get install -y --force-yes \
    curl \
    r-base
    
COPY r_wrapper.sh r_wrapper.sh

ENTRYPOINT ["./r_wrapper.sh"]




