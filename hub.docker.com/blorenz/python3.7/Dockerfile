FROM phusion/baseimage
MAINTAINER blorenz@gmail.com

RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update && apt-get install -y \
        nginx

RUN apt-get update && apt-get install -y \
    python3.7 \
    python3.7-dev \
    libpython3.7-dev \
    python3-pip \
    binutils \
    postgresql-client \
    wget  && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*


RUN apt-get update && apt-get install -y \
    libtiff5-dev libjpeg8-dev \
       libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev \
       #  tcl8.6-dev tk8.6-dev python-tk && \
        zlib1g-dev && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

RUN ln -s $(which python3.7) /usr/local/bin/python
RUN ln -s $(which python3.7) /usr/bin/python
RUN echo 'python3.7 -m pip $*' > /usr/local/bin/pip && chmod 755 /usr/local/bin/pip
RUN pip install --upgrade pip
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /newbuild
RUN mkdir /code/
RUN mkdir /entry/
RUN mkdir /static_files/
RUN mkdir /media_files/

CMD ["/bin/bash"]
