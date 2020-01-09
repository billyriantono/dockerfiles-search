FROM r-base:3.6.1
RUN apt-get update -y && \
    apt-get install -y libcurl4-openssl-dev libxml2-dev openjdk-8-jdk && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*
RUN R CMD javareconf
ADD install.R /
RUN Rscript /install.R
