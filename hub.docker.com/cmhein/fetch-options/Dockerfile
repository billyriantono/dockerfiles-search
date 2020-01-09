FROM rocker/r-ver:3.5.3

RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssh2-1-dev \
    libssl-dev \
    libxml2-dev \
    python-pip \
    zlib1g-dev \
 && rm -rf /var/lib/apt/lists/*

RUN pip install awscli

RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('dplyr')"
RUN Rscript -e "install.packages('lubridate')"
