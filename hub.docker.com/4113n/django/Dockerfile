FROM 4113n/base
MAINTAINER Allen Yu "mail@allenyu.info"

ENV PYTHONUNBUFFERED 1

# R apt repo
RUN sh -c 'echo "deb http://cran.rstudio.com/bin/linux/ubuntu trusty/" >> /etc/apt/sources.list'
RUN gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
RUN gpg -a --export E084DAB9 | apt-key add -

RUN apt-get update && apt-get install -qq -y \
    python-numpy \
    python-scipy \
    libav-tools \
    libblas-dev \
    libfreetype6-dev \
    libffi-dev \
    libjpeg-dev \
    liblapack-dev \
    libpng-dev \
    libpq-dev \
    libtiff5-dev \
    libxml2-dev \
    libxslt1-dev \
    postgresql-client \
    r-base

# Needed by 'pillow' package.
RUN ln -s /usr/lib/x86_64-linux-gnu/libjpeg.so /usr/lib
RUN ln -s /usr/lib/x86_64-linux-gnu/libfreetype.so.6 /usr/lib/libfreetype.so
RUN ln -s /usr/lib/x86_64-linux-gnu/libz.so /usr/lib

# Django service
EXPOSE 80
