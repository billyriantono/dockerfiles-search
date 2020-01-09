FROM dclong/r-base

RUN apt-get update \
    && apt-get install -y \
        libxml2-dev \
        libcairo2-dev \
        libssl-dev \
        libcurl4-openssl-dev \
        libgsl-dev \
        openjdk-8-jdk r-cran-rjava \
    && apt-get autoremove \
    && apt-get autoclean

ADD scripts/ /scripts/
RUN Rscript /scripts/install_packages.r
