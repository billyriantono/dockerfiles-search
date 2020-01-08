FROM r-base:3.5.2
LABEL maintainer="hajo@ventx.de"

# Install packages
RUN apt-get update && apt-get install -y \
    pandoc \
    libssl-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    python3-pip \
 && rm -rf /var/lib/apt/lists/*

# Install R modules
RUN R -e "install.packages('rjson')" && \
    R -e "install.packages('XML')" && \
    R -e "install.packages('xml2')" && \
    R -e "install.packages('charlatan')" && \
    R -e "install.packages('httpuv')" && \
    R -e "install.packages('curl')" && \
    R -e "install.packages('httr')" && \
    R -e "install.packages('shiny')" && \
    R -e "install.packages('rmarkdown')" && \
    R -e "install.packages('knitr')" && \
    R -e "install.packages('caTools')" && \
    R -e "install.packages('writexl')" && \
    R -e "install.packages('rlist')" && \
    R -e "install.packages('tictoc')"&& \
    R -e "install.packages('kableExtra')"
RUN pip3 install awscli
