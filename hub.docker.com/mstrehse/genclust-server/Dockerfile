FROM jcalazan/django
MAINTAINER Maximilian Strehse

RUN apt-get update && apt-get install -y \
    python \
    python-pip \
    python-dev \
    mysql-client \
    libmysqlclient-dev \
    libblas-dev \
    liblapack-dev \
    libatlas-base-dev \
    gfortran \
    build-essential \
    supervisor

RUN pip install numpy
RUN pip install scipy
ADD requirements.txt /
RUN pip install -r requirements.txt

VOLUME /app

WORKDIR /app
