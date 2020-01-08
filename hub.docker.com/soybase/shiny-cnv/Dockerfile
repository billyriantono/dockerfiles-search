FROM rocker/shiny-verse:3.5.1

RUN R -e 'library(devtools); install_github("dicook/phyViz")'

# create directory for logs & bookmarks
WORKDIR /srv/shiny-server
COPY CNV ./CNV/
WORKDIR /var/lib/shiny-server/bookmarks
RUN chown shiny:shiny /var/lib/shiny-server/bookmarks
WORKDIR /var/log/shiny-server
RUN chown shiny:shiny /var/log/shiny-server

EXPOSE 3838
