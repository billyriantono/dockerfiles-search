FROM alpine:3.8
ARG CURATOR_VERSION=5.6.0
RUN apk add --update python py-pip
RUN pip install -U elasticsearch-curator==$CURATOR_VERSION
ENTRYPOINT ["curator"]
