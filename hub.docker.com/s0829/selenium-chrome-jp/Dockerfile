FROM selenium/standalone-chrome
USER root

# install japanese font
RUN apt-get update && \
    apt-get install -y fonts-ipafont-gothic fonts-ipafont-mincho && \
    apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
