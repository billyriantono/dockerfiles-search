# Platform Backend
#
# VERSION 0.1

FROM continuumio/miniconda

MAINTAINER Shaun Irwin <shaun.irwin@gmail.com>

# update conda and setup environment
RUN conda update conda -y \
    && conda create -y -n flask_env python=2.7 pip pandas 

ENV PATH /opt/conda/envs/testenv/bin:$PATH

RUN echo $PATH
RUN conda env list

RUN apt-get update && apt-get install -y \
    pkg-config \
    libpq-dev \
    python-dev

RUN apt-get install -y gcc

RUN /bin/bash -c "source activate /opt/conda/envs/flask_env/ && pip install flask flask-httpauth psycopg2 flask-sqlalchemy flask-migrate"

CMD /bin/bash
