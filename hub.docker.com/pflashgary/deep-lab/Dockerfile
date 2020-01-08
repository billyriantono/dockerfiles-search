FROM nicklarsennz/jupyter-base:2.0.0
USER root

ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal

RUN pip install --upgrade pip && \
    apt update && \
    apt install -y \
        python3-pil \
        python3.7-dev \
        software-properties-common

RUN add-apt-repository ppa:ubuntugis/ppa && \
    apt update && \
    apt install -y gdal-bin libgdal-dev

USER jupyter

COPY requirements.txt .
RUN pip install --user -r requirements.txt
