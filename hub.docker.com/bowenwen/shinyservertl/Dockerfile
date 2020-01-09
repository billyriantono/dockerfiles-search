FROM rocker/shiny-verse

RUN apt-get update -qq && \
    apt-get install -y sudo libudunits2-dev libgdal-dev libproj-dev libgeos-dev libjq-dev libjpeg-dev libssl-dev && \
    R -e "install.packages(c('shinydashboard', 'DT', 'data.table', 'leaflet', 'RColorBrewer', 'plyr', 'googleway', 'plotly'), dependencies = TRUE)"
	