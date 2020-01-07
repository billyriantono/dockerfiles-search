FROM python:3.7.4-alpine

LABEL maintainer="michael.samoylov@gmail.com"

ADD VERSION .

RUN apk add openblas &&\
    apk add --no-cache --virtual .build-deps gcc g++ python3-dev musl-dev gfortran openblas-dev && \
    pip install Cython==0.29.10 numpy==1.16.4 && \
    pip install pandas==0.24.2 scipy==1.3.0 scikit-learn==0.21.2 && \
    apk del .build-deps --no-cache && \
    rm -rf /root/.cache
