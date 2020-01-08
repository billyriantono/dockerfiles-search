FROM jupyter/datascience-notebook

USER root

WORKDIR /tmp

RUN apt-get update \
    && apt-get install -y --no-install-recommends libmysqlclient-dev freetds-dev \
    && rm -rf /var/lib/apt/lists/*

USER jovyan

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /home/jovyan

