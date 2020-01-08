FROM postgres:11.5
RUN apt-get update && \
    apt-get install -y \
    cmake \
    pgxnclient \
    postgresql-server-dev-11 \
    postgresql-plpython-11 \
    g++ \
    m4 \
    patch \
    postgis
ENV PGUSER=postgres
EXPOSE 5432

