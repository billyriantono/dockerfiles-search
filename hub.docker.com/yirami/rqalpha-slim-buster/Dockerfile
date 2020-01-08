FROM yirami/rqalpha-slim-buster:latest as rqalpha_env

ARG MATPLOTLIB_PATH=/usr/local/lib/python3.7/site-packages/matplotlib/mpl-data/fonts/ttf
COPY ./fonts/SimHei.ttf $MATPLOTLIB_PATH/

RUN echo "Install Python package ..." \
    && pip install xlrd \
