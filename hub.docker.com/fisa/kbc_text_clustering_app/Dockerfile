FROM rocker/r-ver:3.4.2

ENV PATH /usr/local/lib/R/bin/:$PATH
ENV R_HOME /usr/local/lib/R

WORKDIR /tmp

# Custom Setup
RUN mkdir /usr/share/doc/R${R_VERSION} \
    && echo 'options(download.file.method = "libcurl")' >> /usr/local/lib/R/etc/Rprofile.site

# Install dependencies for packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        default-jdk \
        ed \
        git \
        libbz2-dev \
        libcairo2-dev \
        libgdal-dev \
        libcgal-dev \
        libglu1-mesa-dev \
        libgsl0-dev \
        libproj-dev \
        libssl-dev \
        libx11-dev \
        libxt-dev \
        xfonts-base \
        unzip \
        x11proto-core-dev \
    && rm -rf /var/lib/apt/lists/*

# install R packages
RUN R -e "install.packages('devtools')"
RUN R -e "devtools::install_github('keboola/r-docker-application', ref = 'master')"
RUN R -e "install.packages('stringdist')"
RUN R -e "install.packages('plyr')"
RUN R -e "install.packages('dplyr')"
RUN R -e "install.packages('stringr')"

# copy code files
COPY main.R /code/main.R

#COPY init.R /code/init.R
#COPY config.json /data/config.json

# install packages
#RUN Rscript /code/init.R

# finally
#RUN R CMD javareconf && /usr/local/lib/R/bin/Rscript /code/main.R
CMD Rscript /code/main.R
