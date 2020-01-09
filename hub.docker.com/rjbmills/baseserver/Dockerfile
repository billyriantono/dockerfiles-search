FROM rocker/r-ver

# Install dependencies and Download and install shiny server
RUN apt-get update && apt-get install -y \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    xtail \
    libssl-dev \
    libgdal-dev \
    libxml2-dev \
    curl \
    wget \
    cron

RUN sudo rm -rf /var/lib/apt/lists/*

# Download and install shiny server
RUN wget --no-verbose https://download3.rstudio.org/ubuntu-14.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    . /etc/environment && \
    R -e "install.packages(c('shiny', 'rmarkdown'), repos='https://cran.rstudio.com/')" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    chown shiny:shiny /var/lib/shiny-server

# Install Database related apt
RUN apt-get update -y && apt-get -f install -y --no-install-recommends \
    libaio1

RUN R -e "install.packages(c( \
    'data.table', \
    'dplyr', \
    'DT', \
    'DBI', \
    'XML', \
    'rJava',\ 
    'devtools', \
    'RPostgreSQL', \
    'ggthemes', \
    'rCharts', \
    'htmlwidgets', \
    'httr', \
    'jsonlite', \
    'lubridate', \
    'openxlsx', \
    'RJSONIO', \
    'RCurl', \
    'RForcecom', \
    'pool', \
    'scales', \
    'shinyjs', \
    'stringr', \
    'svglite', \
    'logging', \
    'shinyjs', \
    'shinythemes', \
    'plotly', \
    'remotes', \
    'aws.s3', \
    'salesforcer'), repos='https://cran.rstudio.com/')" \
  && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

  RUN R -e "devtools::install_github('hadley/ggplot2')" \
  && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

ADD https://github.com/just-containers/s6-overlay/releases/download/v1.21.4.0/s6-overlay-amd64.tar.gz /tmp/

RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /