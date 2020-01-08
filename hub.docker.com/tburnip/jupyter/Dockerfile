FROM alpine:latest
RUN apk update && apk add g++ make subversion gcc gfortran ca-certificates python3-dev libpng-dev freetype-dev python3; ln -s /usr/include/locale.h /usr/include/xlocale.h
WORKDIR /usr/src/app
COPY requirements.txt ./
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install --no-cache-dir -r requirements.txt
RUN rm requirements.txt
COPY jupyter_notebook_config.py /root/.jupyter/