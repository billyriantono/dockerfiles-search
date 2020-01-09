FROM continuumio/miniconda3:4.6.14

USER root

RUN apt update\
    && apt install -y\
    curl git unzip

WORKDIR /var/geocode

RUN curl -O https://www1.nyc.gov/assets/planning/download/zip/data-maps/open-data/linux_geo19b_19_2.zip\
    && unzip *.zip\
    && rm *.zip

RUN mkdir linux_upad_tpad_19b2\
    && curl -o linux_upad_tpad_19b2/linux_upad_tpad_19b2.zip https://www1.nyc.gov/assets/planning/download/zip/data-maps/open-data/linux_upad_tpad_19b2.zip\
    && unzip -o linux_upad_tpad_19b2/*.zip -d version-19b_19.2/fls/\
    && rm -r linux_upad_tpad_19b2
    
ENV GEOFILES=/var/geocode/version-19b_19.2/fls/
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/var/geocode/version-19b_19.2/lib/

RUN pip install --upgrade pip\
    && pip install python-geosupport
