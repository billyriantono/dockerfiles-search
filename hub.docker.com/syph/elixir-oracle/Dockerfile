FROM elixir:1.6-slim

LABEL maintainer="Bruno Louvem <btlouvem@gmail.com>"
LABEL version="0.0.1"

ENV ORACLE_HOME=/usr/local/instantclient_12_2
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:${ORACLE_HOME}
ENV CFLAGS=-m64
ENV PATH=${PATH}:/usr/local/unixODBC/bin
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/unixODBC/lib:/opt/oracle/instantclient_12_2
ENV TERM=xterm-256color

ADD unix*.tar.gz /root/
ADD instantclient-*.zip /root/
ADD odbc*.ini /root/

RUN echo "$(tput setaf 13)Install linux dependencies $(tput sgr0)" && \
    apt-get update && apt-get install -qy --no-install-recommends g++ gcc make zip unzip libaio1 curl ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "$(tput setaf 13)Install dockerize $(tput sgr0)" && \
    curl --silent --show-error --location --fail --retry 3 --output /tmp/dockerize-linux-amd64.tar.gz \
    https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/dockerize-latest.tar.gz && \
    tar -C /usr/local/bin -xzvf /tmp/dockerize-linux-amd64.tar.gz && \
    rm -rf /tmp/dockerize-linux-amd64.tar.gz && \
    dockerize --version && \
    echo "$(tput setaf 13)Moving unixODBC and oracle client files $(tput sgr0)" && \
    mkdir -p /usr/local/unixODBC/etc && mkdir /opt/oracle && \
    mv /root/unixODBC-2.3.5 /usr/local/unixODBC/ && \
    cp /root/instantclient-basic-linux.zip /opt/oracle/instantclient-basic-linux.zip && \
    cd /opt/oracle && \
    unzip instantclient-basic-linux.zip && \
    cd /opt/oracle/instantclient_12_2 && \
    ln -s libclntsh.so.12.1 libclntsh.so && \
    ln -s libocci.so.12.1 libocci.so && \
    echo /opt/oracle/instantclient_12_2 > /etc/ld.so.conf.d/oracle-instantclient.conf && \
    ldconfig && \
    rm -f /root/instantclient-basic-linux.zip && \
    rm -f /opt/oracle/instantclient-basic-linux.zip && \
    cp /root/instantclient-odbc-linux.zip /usr/local/instantclient-odbc-client.zip && \
    cd /usr/local && \
    unzip instantclient-odbc-client.zip && \
    rm -f /root/instantclient-odbc-linux.zip && \
    rm -f /usr/local/instantclient-odbc-client.zip && \
    cd /usr/local/unixODBC/unixODBC-2.3.5 && \
    mv /root/odbc*.ini /usr/local/unixODBC/etc/ && \
    echo "$(tput setaf 13)Install unixODBC $(tput sgr0)" && \
    ./configure --prefix=/usr/local/unixODBC && \
    make && make install
