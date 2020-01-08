FROM rocker/shiny-verse:3.5.1

RUN R -e 'library(devtools); install_github("dicook/phyViz")'
RUN R -e 'install.packages("knitrBootstrap")'

# create directory for logs & bookmarks
WORKDIR /srv/shiny-server
COPY Genealogy ./Genealogy/
WORKDIR Genealogy/
RUN R -e 'library(knitrBootstrap); library(rmarkdown); render("Documentation.Rmd", "knitrBootstrap::bootstrap_document")' \
    && rm -rf /tmp/downloaded_packages
WORKDIR /var/lib/shiny-server/bookmarks
RUN chown shiny:shiny /var/lib/shiny-server/bookmarks
WORKDIR /var/log/shiny-server
RUN chown shiny:shiny /var/log/shiny-server

EXPOSE 3838
