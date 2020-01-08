# @edt ASIX M11 Curs 2017-2018
# postgres:base 
# servidor postgres
# ----------------------------------

FROM postgres:9.3
MAINTAINER @isx45128227 "Roger Ferran @edt Curs 2017-2018"
ENV POSTGRES_USER docker
ENV POSTGRES_PASSWORD jupiter
ENV POSTGRES_DB training
# COPY pg_hba.conf /var/lib/postgresql/data/
# RUN echo "host    all             all             172.17.0.2/32           trust" >> /var/lib/postgresql/data/pg_hba.conf
# RUN echo "host    all             all             0.0.0.0/0               trust" >> /var/lib/postgresql/data/pg_hba.conf
# ADD pg_hba.conf /var/lib/postgresql/data/
EXPOSE 5432
ADD training/script-training.sql /docker-entrypoint-initdb.d/
