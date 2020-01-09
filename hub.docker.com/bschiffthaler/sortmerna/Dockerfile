FROM alpine AS alpine-build-sortmerna

ARG SORTMERNA_VERSION=4.0.0

WORKDIR /build
RUN apk update && apk add curl bash

WORKDIR /build
RUN curl -O -L https://github.com/biocore/sortmerna/releases/download/v${SORTMERNA_VERSION}/sortmerna-${SORTMERNA_VERSION}-Linux.sh
RUN bash sortmerna-${SORTMERNA_VERSION}-Linux.sh --skip-license

FROM alpine 

ARG SORTMERNA_VERSION=4.0.0

WORKDIR / 
COPY --from=alpine-build-sortmerna /build/bin/sortmerna /usr/local/bin/sortmerna
ENTRYPOINT ["/usr/local/bin/sortmerna"]

LABEL maintainer='github.com/bschiffthaler'
LABEL software.version=${SORTMERNA_VERSION}
