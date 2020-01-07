FROM ubuntu:14.04
MAINTAINER Barry Martin - nyxcharon@gmail.com
RUN apt-get -y update && apt-get -y install \
    git  \     
    emacs \	
    python2.7 \
    python-dev \
    python-pip \
    # Pillow libraries
    python-tk \ 
    libtiff5-dev \
    libjpeg8-dev \
    libfreetype6-dev \
    liblcms2-dev \
    libwebp-dev \
    tcl8.6-dev \
    tk8.6-dev \ 
    zlib1g-dev
    # End Pillow Libraries
RUN pip install django==1.7
EXPOSE 8000


