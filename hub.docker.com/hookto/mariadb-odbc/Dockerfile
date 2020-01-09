FROM debian:stretch-slim

ENV DEBIAN_FRONTEND=noninteractive

ENV SRC_DIR=/build

ENV MARIADB_ODBC_DRIVER_SRC_SUBDIR=mariadb-connector
ENV MARIADB_DRIVER_TAG="v3.0.2"
ENV MARIADB_CONNECTOR_SRC=${SRC_DIR}/${MARIADB_ODBC_DRIVER_SRC_SUBDIR}


## MariaDB ODBC Driver from sources

RUN apt-get update && \
    apt-get install -y \
        curl \
        unixodbc \
        unixodbc-dev \
        odbcinst \
        cmake \
        build-essential \
        libssl1.0-dev \
        mariadb-client && \
    mkdir -p ${SRC_DIR} && \
    cd ${SRC_DIR} && \
    URL="https://api.github.com/repos/MariaDB/mariadb-connector-c/tarball/${MARIADB_DRIVER_TAG}" && \
    curl -o file.tar.gz -L $URL && \
    tar -xvzf file.tar.gz && \
    rm file.tar.gz && \
    mv ./MariaDB-* ${MARIADB_ODBC_DRIVER_SRC_SUBDIR} && \
    cd ${MARIADB_CONNECTOR_SRC} && \
    cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=/usr/local -LH && \
    make && \
    make install && \
    rm -rf ${MARIADB_CONNECTOR_SRC}
    
    