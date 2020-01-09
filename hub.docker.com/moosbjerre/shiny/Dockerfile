FROM rocker/r-ver:3.6.0

RUN apt-get update && apt-get install -y \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    xtail \
    wget

# COPY installmbr.sh /usr/local/bin/installmbr.sh
COPY mb_1.0.2.tar.gz /usr/local/bin/

# Download and install shiny server
RUN wget --no-verbose https://download3.rstudio.org/ubuntu-14.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    . /etc/environment && \
    # Install R packages
    R -e "install.packages(c('RJSONIO', 'DBI', 'stringr'), repos='$MRAN')" && \
    R -e "install.packages('/usr/local/bin/mb_1.0.2.tar.gz', repos = NULL, type = 'source')" && \
    R -e "install.packages(c('shiny' ,'DT' ,'questionr' ,'rsconnect' ,'rmarkdown' ,'survey' ,'rdrop2' ,'curl' ,'openxlsx'), repos='$MRAN')" && \
    # chmod +x /usr/local/bin/installmbr.sh && /usr/local/bin/installmbr.sh && \
    # R -e "install.packages(c('shiny', 'rmarkdown'), repos='$MRAN')" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    chown shiny:shiny /var/lib/shiny-server

EXPOSE 3838

# Copy the actual app
COPY /mb-svarmonitorering /srv/shiny-server/mb-svarmonitorering

COPY shiny-server.sh /usr/bin/shiny-server.sh

# Prepare tool log
RUN mkdir /srv/shiny-server/mb-svarmonitorering/debug && \
  touch /srv/shiny-server/mb-svarmonitorering/debug/log.txt

CMD ["/usr/bin/shiny-server.sh"]
