FROM python:2.7.14-alpine3.7

WORKDIR /tmp

RUN apk update \
 && apk add wget ca-certificates \
 && apk add build-base \
 && apk add gcc gfortran build-base freetype-dev libpng-dev openblas-dev

RUN ln -s /usr/include/locale.h /usr/include/xlocale.h

RUN rm -rf /tmp/*
RUN rm -rf /var/cache/apk/*

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN pip install "statsmodels < 0.8.0"
RUN pip install "numpy >= 1.7.1"
RUN pip install "matplotlib >= 2.1.1"
RUN pip install "pandas >= 0.22.0"
RUN pip install "scikit-learn >= 0.19.1"
