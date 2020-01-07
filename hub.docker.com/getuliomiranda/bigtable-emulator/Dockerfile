FROM google/cloud-sdk:alpine
MAINTAINER Getulio Miranda "getulio.miranda2@gmail.com"

RUN gcloud components install bigtable \
    && gcloud components update beta

ARG BIGTABLE_HOST

EXPOSE 8086

ENTRYPOINT gcloud beta emulators bigtable start --host-port=$BIGTABLE_HOST:8086 --quiet
