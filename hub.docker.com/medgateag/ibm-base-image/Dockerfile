From ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install --fix-missing -y \
    unzip \
    git \
    curl \
    vim \
    sudo \
    nginx \
    supervisor \
    python3 \
    virtualenv \
    python3-pip \
    uwsgi-plugin-python \
    libgfortran3 \
    gfortran \
    nmon \
    language-pack-en \
    cron \
    && apt-get -qy autoremove \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8

RUN pip3 install --upgrade pip

RUN adduser --disabled-password --gecos '' aida

RUN mkdir -p /home/aida/etc/

RUN ["/bin/bash", "-c", "cd /home/aida/etc/ && virtualenv --python=/usr/bin/python3 --system-site-packages aite-api-env && source /home/aida/etc/aite-api-env/bin/activate && pip install uwsgi && deactivate"]

COPY ibm-base-image.version /home/aida/

COPY requirements.txt /tmp
RUN pip3 install numpy==1.13.3
RUN pip3 install -r /tmp/requirements.txt

# nginx config
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
