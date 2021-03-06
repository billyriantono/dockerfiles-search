#ARG POSTGRES_VERSION
FROM postgres:12.1-alpine

# install citus
ARG VERSION=9.1.0
LABEL maintainer="Citus Data https://citusdata.com" \
      org.label-schema.name="Citus" \
      org.label-schema.description="Scalable PostgreSQL for multi-tenant and real-time workloads" \
      org.label-schema.url="https://www.citusdata.com" \
      org.label-schema.vcs-url="https://github.com/citusdata/citus" \
      org.label-schema.vendor="Citus Data, Inc." \
      org.label-schema.version=${VERSION}-alpine \
      org.label-schema.schema-version="1.0"
 
 RUN apk add --no-cache \
            --virtual builddeps \
        build-base \
        curl \
        curl-dev \
        openssl-dev \
        ca-certificates \
        tar \
        clang \
        llvm \    
        icu-dev && \
    apk add --no-cache libcurl && \
    curl -sfLO "https://github.com/citusdata/citus/archive/v${VERSION}.tar.gz" && \
    tar xzf "v${VERSION}.tar.gz" && \
    cd "citus-${VERSION}" && \
    ./configure && \
    make install && \
    cd .. && \
    rm -rf "citus-${VERSION}" "v${VERSION}.tar.gz" && \
    apk del builddeps
    
# install POSTGIS
#ARG POSTGIS_VERSION
#ARG POSTGIS_SHA256

ENV POSTGIS_VERSION 2.5.2
ENV POSTGIS_SHA256 225aeaece00a1a6a9af15526af81bef2af27f4c198de820af1367a792ee1d1a9

RUN  wget -O postgis.tar.gz  "https://github.com/postgis/postgis/archive/$POSTGIS_VERSION.tar.gz"  \
    && echo "$POSTGIS_SHA256 *postgis.tar.gz" | sha256sum -c - \
    && mkdir -p /usr/src/postgis \
    && tar \
        --extract \
        --file postgis.tar.gz \
        --directory /usr/src/postgis \
        --strip-components 1 \
&& rm postgis.tar.gz 

RUN apk add \
	--no-cache \
	--virtual .build-deps \
		autoconf \
		automake \
		clang-dev \
		json-c-dev \
		libtool \
		libxml2-dev \
		llvm8 \
		make \
		perl \
&& apk add \
	--no-cache \
	--virtual .build-deps-edge \
	--repository http://dl-cdn.alpinelinux.org/alpine/edge/main \
	--repository http://dl-cdn.alpinelinux.org/alpine/edge/community \
		g++ \
		gdal-dev \
		geos-dev \
		proj-dev \
		protobuf-c-dev \
&& cd /usr/src/postgis \
&& ./autogen.sh \
&& ./configure \
&& make \
&& make install \
&& cd / \
&& rm -r /usr/src/postgis \
&& apk del \
	.build-deps \
	.build-deps-edge \
&& apk add \
	--no-cache \
	--virtual .postgis-rundeps \
		json-c \
&& apk add \
	--no-cache \
	--virtual .postgis-rundeps-edge \
	--repository http://dl-cdn.alpinelinux.org/alpine/edge/main \
	--repository http://dl-cdn.alpinelinux.org/alpine/edge/community \
		geos \
		gdal \
		proj \
		protobuf-c

COPY  ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY  ./update-postgis.sh /usr/local/bin
    
# add citus to default PostgreSQL config
RUN echo "shared_preload_libraries='citus'" >> /usr/local/share/postgresql/postgresql.conf.sample

# add scripts to run after initdb
COPY 000-configure-stats.sh 001-create-citus-extension.sql /docker-entrypoint-initdb.d/

# add health check script
COPY pg_healthcheck /

HEALTHCHECK --interval=4s --start-period=6s CMD ./pg_healthcheck
