FROM ubuntu:latest as builder

    # install build packages
    RUN apt-get update \
        && apt-get install -y --no-install-recommends \
            build-essential \
            cmake \
        && rm -rf /var/lib/apt/lists/*

    # set work directory
    WORKDIR /opt/firebird-tpcc

    # copy RedDatabase from rdb image
    COPY --from=xabbl4/red-database /opt/RedDatabase /opt/RedDatabase
    ENV FB_ROOT_DIR=/opt/RedDatabase
    
    # copy and compile TPC-C
    COPY ./sql ./sql
    COPY ./src ./src
    COPY ./CMakeLists.txt ./
    RUN cmake .
    RUN make

FROM ubuntu:latest

    # install need packages
    RUN apt-get update \
        && apt-get install -y --no-install-recommends \
            libtommath1 \
            libgssapi-krb5-2 \
        && rm -rf /var/lib/apt/lists/*

    RUN ln -s /usr/lib/x86_64-linux-gnu/libtommath.so.1.0.1 /usr/lib/x86_64-linux-gnu/libtommath.so.0
    COPY --from=builder /opt/RedDatabase /opt/RedDatabase
    COPY --from=builder /opt/firebird-tpcc/bin/tpcc /opt/firebird-tpcc/bin/
    COPY --from=builder /opt/firebird-tpcc/bin/load /opt/firebird-tpcc/bin/
    COPY --from=builder /opt/firebird-tpcc/sql/. /opt/firebird-tpcc/sql/

    # set work directory
    WORKDIR /opt/firebird-tpcc

    COPY docker-entrypoint.sh /usr/local/bin/
    RUN ln -s /usr/local/bin/docker-entrypoint.sh / # backwards compat
    ENTRYPOINT ["docker-entrypoint.sh"]
