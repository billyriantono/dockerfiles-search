FROM rocker/shiny-verse:3.6.1

MAINTAINER Nicole Kauer nmekauer@gmail.com

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libasound2 \
    libdbus-glib-1-2 libgtk2.0-0 libpango1.0-0 libxt6 wget bzip2 sudo

# Install Firefox
RUN mkdir /application
RUN cd /application; wget -O - \
    http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/25.0/linux-x86_64/en-US/firefox-25.0.tar.bz2 | tar jx

RUN apt-get update && apt-get -y install \ 
    build-essential python3-all python3-pip libncurses5-dev libncursesw5-dev libzmq3-dev \
    && pip3 install --upgrade pip \
    && pip install jupyter \
    && apt-get -y remove build-essential \
    && apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN R -e "install.packages(c('IRdisplay', 'repr', 'devtools', 'evaluate', 'crayon', 'config', 'pbdZMQ', 'uuid', 'digest', 'BiocManager', 'stringr', 'RColorBrewer', 'Cairo', 'GlobalOptions', 'boot', 'foreign', 'mgcv', 'nlme', 'shinydashboard'),repos = 'http://cran.us.r-project.org'); BiocManager::install(\"ComplexHeatmap\")"

ENV BROWSER /application/firefox/firefox

COPY . /FILES

CMD ["/bin/sh"]