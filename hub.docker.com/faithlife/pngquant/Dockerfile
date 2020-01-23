FROM debian:9 AS build

RUN apt-get update \
  && apt-get install -y \
    build-essential \
    curl \
    libpng-dev \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/src

ARG PNGQUANT_VERSION=2.12.2
RUN curl -LOsS http://pngquant.org/pngquant-${PNGQUANT_VERSION}-src.tar.gz \
  && tar xf pngquant-${PNGQUANT_VERSION}-src.tar.gz \
  && rm pngquant-${PNGQUANT_VERSION}-src.tar.gz

WORKDIR /usr/local/src/pngquant-${PNGQUANT_VERSION}
RUN ./configure --extra-cflags=-static \
  && make \
  && make install

FROM debian:9-slim

COPY --from=build /usr/local/bin/pngquant /usr/local/bin/
