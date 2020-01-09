FROM rocker/r-base

MAINTAINER Jacob Cardenas "jcardenas256@gmail.com"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    sudo \
    xorg \
    libx11-dev \
    libglu1-mesa-dev \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libssl-dev \
    libssh2-1-dev \
    default-jre \
    default-jdk \
    libxml2 \
    libxml2-dev

# install app package dependencies
RUN R -e "install.packages(c('shiny','shinydashboard','ggplot2','RColorBrewer','fastcluster','NMF','clValid','VennDiagram','gtools','scales','reshape2','data.table', 'shinyjs','stringr','DT','dplyr','pca3d'),repos='https://cloud.r-project.org/')"

# copy the app to the image
RUN mkdir /root/BART
COPY BART /root/BART

COPY Rprofile.site /usr/lib/R/etc/

EXPOSE 3838

CMD ["R", "-e shiny::runApp('/root/BART')"]
