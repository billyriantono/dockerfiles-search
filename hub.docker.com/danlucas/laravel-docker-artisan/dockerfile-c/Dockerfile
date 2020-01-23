FROM python:3.6.6-alpine3.8
RUN apk --no-cache add --virtual .builddeps g++ gcc gfortran musl-dev lapack-dev \
 && pip install numpy==1.14.3 \
 && pip install scipy==1.1.0 \
 && pip install scikit-learn==0.19.2 \
 && pip install pandas==0.23.4 \
 && apk del .builddeps \
 && rm -rf /root/.cache

