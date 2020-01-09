# Build
FROM debian:buster

RUN apt-get update \
    && apt-get -y install git clang cmake make gcc g++ libmariadbclient-dev libssl-dev libbz2-dev libreadline-dev libncurses-dev libboost-all-dev p7zip default-libmysqlclient-dev git \
    && update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100 \
    && update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang 100

WORKDIR /src
RUN git clone -b 3.3.5 git://github.com/TrinityCore/TrinityCore.git . \
    && mkdir build \
    && cd build \
    && cmake ../ -DCMAKE_INSTALL_PREFIX=/app -DTOOLS=1 \
    && mkdir /app \
    && make \
    && make install



# Run
FROM debian:buster
ENV PATH "/app/bin:${PATH}"

WORKDIR /app
COPY --from=0 /app /app/
COPY --from=0 /src/sql /app/sql
RUN mkdir /app/data
VOLUME /app/data

RUN apt-get update \
    && apt-get -y install \
       libssl1.1 \
       libreadline7 \
       libboost-system1.67.0 \
       libboost-filesystem1.67.0 \
       libboost-thread1.67.0 \
       libboost-program-options1.67.0 \
       libboost-iostreams1.67.0 \
       libboost-regex1.67.0 \
       mariadb-client \
       nano \
       p7zip \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 3724/tcp
EXPOSE 8085/tcp
EXPOSE 8085/udp

CMD tail -f /dev/null
