FROM python:3.8.0a3-alpine3.9

USER root

RUN apk add curl git unzip make automake gcc g++ subversion python3-dev

WORKDIR /var/geocode

RUN curl -O https://www1.nyc.gov/assets/planning/download/zip/data-maps/open-data/linux_geo19b_19_2.zip\
    && unzip *.zip\
    && rm *.zip

ENV GEOFILES=/var/geocode/version-19b_19.2/fls/
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/var/geocode/version-19b_19.2/lib/

RUN pip install --upgrade pip\
    && pip install python-geosupport flask 

EXPOSE 5000
