FROM ubuntu:xenial

MAINTAINER Jason Mark "jason.mark.01@gmail.com"

RUN apt-get update && apt-get install -y \
    r-base \
    wget \
    gdebi-core \
    libssl-dev \
    sqlite3 \
    libsqlite3-dev

# Install R packages
RUN R -e "install.packages('shiny', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('rmarkdown', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('shinythemes', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('shinydashboard', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('dplyr', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('scales', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('lubridate', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('ggplot2', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('labeling', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('reshape2', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('gridExtra', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('DT', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('forcats', repos='http://cran.rstudio.com/')" && \
    R -e "install.packages('RSQLite', repos='http://cran.rstudio.com/')" && \
    R -e "options(repos='http://cran.rstudio.com/');"


# Download and install Shiny Server
WORKDIR /tmp/
RUN wget http://download3.rstudio.org/ubuntu-12.04/x86_64/shiny-server-1.5.0.831-amd64.deb && \
    gdebi -n shiny-server-1.5.0.831-amd64.deb && \
    rm shiny-server-1.5.0.831-amd64.deb

EXPOSE 3838

ENV LANG en_US.UTF-8

# TODO: This needs to be fixed/updated to use a passed UID value, but this works for testing.

# shiny user is created by the Shiny Server package installed above
# Change the UID/GID of shiny user/group, ownership of files and start
# shiny-server
RUN groupmod -g 1000 shiny && \
    usermod -u 1002 shiny && \
    chown -R 1002:1000 /home/shiny && \
    chown -R 1002:1000 /var/log/shiny-server && \
    chown -R 1002:1000 /srv/shiny-server && \
    chown -R 1002:1000 /var/lib/shiny-server
    
CMD ["/usr/bin/shiny-server"]