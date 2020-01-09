FROM rocker/tidyverse:3.6.0

RUN apt update && apt install -y \
    libfftw3-dev \
    libtiff-dev \
    libx11-dev \
    libxt-dev \
    python3-pip \
 && apt clean \
 && rm -rf /var/lib/apt/lists/*

RUN pip3 install rawpy

RUN install2.r --error \
    imager \
    reticulate \
 && rm -rf /tmp/downloaded_packages/
