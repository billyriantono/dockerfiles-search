FROM r-base:latest

MAINTAINER Chad Jones "chad@crashcode.org"

# Install dependencies and Download and install shiny server
RUN apt-get update && apt-get install -y -t unstable \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev/unstable \
    openjdk-8-jdk \
    r-cran-rodbc \
    unixodbc \
    unixodbc-dev \
    freetds-bin \
    freetds-common \
    freetds-dev \
    libct4 \
    libsybdb5 \
    tdsodbc \
    sqsh \
    libxt-dev && \
    useradd -u 1001 shiny && \
    wget --no-verbose https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    R CMD javareconf && \
    R -e "install.packages(c('shiny', 'rmarkdown', 'varhandle', 'gridExtra', 'grid', 'XLConnect', 'RODBC', 'shinydashboard', 'rJava', 'rhandsontable', 'qcc', 'DT', 'ggplot2', 'dplyr', 'magrittr', 'xlsx', 'openxlsx', 'sqldf', 'RH2', 'lubridate', 'tidyr', 'forecast'), repos='https://cran.rstudio.com/')" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 3838

COPY odbc.ini /etc/odbc.ini
COPY odbcinst.ini /etc/odbcinst.ini
COPY freetds.conf /home/shiny/.freetds.conf
COPY shiny-server.sh /usr/bin/shiny-server.sh
COPY shiny-server.conf /etc/shiny-server/shiny-server.conf

RUN ["chmod", "+x", "/usr/bin/shiny-server.sh"]
RUN ["chown", "shiny:shiny", "/home/shiny/.freetds.conf"]
RUN ["chown", "shiny:shiny", "/srv/shiny-server"]

ENTRYPOINT shiny-server.sh


