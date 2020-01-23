FROM python:3.7-alpine3.10

# need to update libressl first so other packages will install later.
# adding libc6-compat to allow for AWS built binaries to run in this instance.
RUN apk update && \
    apk add -u \
    libressl \
    libc6-compat

# install required packages for psycopg2 pillow postgis
RUN apk add -u \
    postgresql-dev \
    gcc \
    g++ \
    python3-dev \
    musl-dev \
    libffi-dev \
    jpeg-dev \
    zlib-dev \
    libmemcached-dev \
    libffi-dev \
    tiff-dev \
    openjpeg-dev \
    libpng-dev \
    freetype-dev \
    lcms2-dev \
    libwebp-dev \
    curl

# install packages from testing
RUN apk add \
    --no-cache \
    --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
    --repository http://dl-cdn.alpinelinux.org/alpine/edge/main \
    gdal-dev \
    geos-dev \
    protobuf-c-dev \
    gdal


ENV PYTHON_LOG_LEVEL warning

ENV PYTHONUNBUFFERED 0

ENV SYS_ENVIRONMENT=docker
ENV CODE_ENVIRONMENT=default

WORKDIR /usr/src/app

EXPOSE 8000

CMD './docker_start.sh'
