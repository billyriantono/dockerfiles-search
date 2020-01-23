FROM python:3.7-alpine

RUN apk update
RUN apk add --virtual build-deps gcc musl-dev
RUN apk --no-cache --update-cache add gcc gfortran python python-dev py-pip build-base wget freetype-dev libpng-dev openblas-dev
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h
RUN pip3 install pandas==0.23.4 &&\
    pip3 install matplotlib==3.0.2 &&\
    pip3 install xlrd==1.2.0 &&\
    pip3 install scipy==1.2.0 &&\
    pip3 install scikit-learn==0.20.2

RUN mkdir -p /root/.config/matplotlib
RUN echo "backend : Agg" > /root/.config/matplotlib/matplotlibrc

COPY wait /bin/wait-for-ports
RUN apk del build-deps
