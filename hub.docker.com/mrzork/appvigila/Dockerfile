FROM openanalytics/r-base

MAINTAINER Camilo Herrera "camiloherrera.co"

# system libraries of general use
RUN apt-get update && apt-get install -y \
    sudo \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libssl1.0.0 

# system library dependency for the Redes app
RUN apt-get update && apt-get install -y \
    libprotobuf-dev \
    libgeos-dev \
    protobuf-compiler \
    libv8-dev \
    libproj-dev \
    libgdal-dev  \
    libv8-dev \
    libgdal1-dev  \
    libudunits2-dev \
    libspatialite-dev \
    libgdal1i

# basic shiny functionality
RUN R -e "install.packages(c('shiny', 'rmarkdown'), repos='https://cloud.r-project.org/')"

# install dependencies of the Redes app

RUN R -e "install.packages(c('devtools','RColorBrewer','shinyBS','shinycssloaders','scales','shinydashboard','sp','dplyr','xts','tidyr','DT','lubridate','ggplot2','ggvis','data.table','leaflet','V8','plotly','rintrojs'), repos='https://cloud.r-project.org/')"
RUN R -e "devtools::install_github('RcppCore/Rcpp')"
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y "ppa:marutter/rrutter"
RUN add-apt-repository -y "ppa:marutter/c2d4u"
RUN apt-get update     # now with new repos
RUN apt-get install -y r-cran-readr
RUN R -e "devtools::install_github('hadley/ggplot2')"

RUN add-apt-repository -y "ppa:ubuntugis/ubuntugis-unstable"
RUN apt-get update
RUN apt-get install -y libgdal-dev libgeos-dev libproj-dev libudunits2-dev liblwgeom-dev

RUN R -e "install.packages(c('rgdal','rgeos','jsonlite','geojson','geojsonio','rgdal') ,repos='https://cloud.r-project.org/',dependencies=TRUE)"

# copy the app to the image
RUN mkdir /root/appvigila
COPY appvigila /root/appvigila

COPY Rprofile.site /usr/lib/R/etc/

EXPOSE 3838

CMD ["R", "-e shiny::runApp('/root/appvigila')"]

