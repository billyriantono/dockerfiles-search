FROM        ubuntu:18.04

WORKDIR     /tmp/workdir

RUN     apt-get -yqq update &&  \
        apt-get --no-install-recommends -yqq install r-base && \
        rm -rf /var/lib/apt/lists/*

RUN     apt-get -yqq update && \
        apt-get --no-install-recommends -yqq install curl unzip make autoconf automake cmake g++ gcc  && \
        rm -rf /var/lib/apt/lists/*

RUN     R -e "install.packages('ggplot2', repos = 'http://cran.us.r-project.org')"

MAINTAINER  Colin McFadden <mcfa0086@umn.edu>

CMD         ["--help"]
ENTRYPOINT  ["R"]
ENV         LD_LIBRARY_PATH=/usr/local/lib
