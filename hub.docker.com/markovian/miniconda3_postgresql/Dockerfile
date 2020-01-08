FROM continuumio/miniconda3

RUN echo "Installing system requirements ..." \
    && wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | apt-key add - \
    && echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" >> /etc/apt/sources.list.d/pgdg.list \
    && apt-get update \
    && apt-get --yes install postgresql postgresql-contrib
