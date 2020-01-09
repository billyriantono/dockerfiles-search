FROM rocker/r-ver:3.5.3

RUN apt-get update && apt-get install -y \
    libcairo2-dev \
    libcurl4-openssl-dev \
    libssh2-1-dev \
    libssl-dev \
    libxml2-dev \
    python-pip \
    zlib1g-dev \
 && rm -rf /var/lib/apt/lists/*

RUN pip install awscli

RUN Rscript -e "install.packages('glue')" # must precede devtools install
RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('dplyr')"
RUN Rscript -e "install.packages('extrafont')"
RUN Rscript -e "install.packages('ggbeeswarm')"
RUN Rscript -e "install.packages('ggplot2')"
RUN Rscript -e "install.packages('ggpubr')"
RUN Rscript -e "install.packages('gtable')"
RUN Rscript -e "install.packages('hrbrthemes')"
RUN Rscript -e "install.packages('lubridate')"
RUN Rscript -e "install.packages('magrittr')"
RUN Rscript -e "install.packages('purrr')"
RUN Rscript -e "install.packages('Quandl')"
RUN Rscript -e "install.packages('scales')"
RUN Rscript -e "install.packages('tidyr')"
RUN Rscript -e "install.packages('TTR')"
RUN Rscript -e "install.packages('viridis')"

