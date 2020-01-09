FROM fabarca/ocpu-rstudio-spatial

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    xtail \
    && rm -rf /var/lib/apt/lists/*

RUN wget --no-verbose https://download3.rstudio.org/ubuntu-14.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    . /etc/environment && \
    R -e "install.packages(c('shiny', 'rmarkdown'))" && \
    rm /srv/shiny-server/index.html && \
    rm -rf /srv/shiny-server/sample-apps
#    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/

RUN R -e "install.packages(c('shinycssloaders', 'rsample'))"

EXPOSE 3838

COPY shiny-server.sh /usr/bin/shiny-server.sh

CMD ["/usr/bin/shiny-server.sh"]

