FROM rocker/tidyverse:3.5.1

## rserve
RUN apt-get update \
  && apt-get install -y libssl-dev wget curl procps \
  && wget https://www.rforge.net/src/contrib/Rserve_1.8-6.tar.gz \
  && /usr/local/bin/R CMD INSTALL Rserve_1.8-6.tar.gz

## chainladder
RUN apt-get install -y libnlopt-dev
RUN R -e 'install.packages(c("ChainLadder"))'

RUN mkdir -p /etc/services.d/rserve \
    && echo '#!/usr/bin/with-contenv sh \n /usr/local/bin/R CMD Rserve --slave --RS-conf /home/rstudio/rserve.conf --RS-source /home/rstudio/rserve-src.R' > /etc/services.d/rserve/run

EXPOSE 8000

CMD ["/init"]
