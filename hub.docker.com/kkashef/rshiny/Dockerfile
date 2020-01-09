FROM rocker/shiny

MAINTAINER Kamran Kashef "kamrankashef@a.com"

# Install dependencies and Download and install shiny server
RUN apt-get update && apt-get install -y -t unstable \
    openjdk-8-jdk \
    libssl-dev \
    r-cran-rjava && \
    R -e "install.packages('RJDBC',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('properties',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('httr',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('leaflet',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('dplyr',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('shinydashboard',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('curl',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('jsonlite',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('ggplot2',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('DT',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('tidyr',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('shinythemes',dep=TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "install.packages('rpivotTable',dep=TRUE, repos='https://cran.rstudio.com/')"

#EXPOSE 3838

#COPY shiny-server.sh /usr/bin/shiny-server.sh

#CMD ["/usr/bin/shiny-server.sh"]
