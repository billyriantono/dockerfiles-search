FROM google/cloud-sdk:alpine

LABEL maintainer="Game Server Services, Inc. <contact@gs2.io>"

ENV CLOUDSDK_CORE_PROJECT gs2
ENV PORT 8000
ENV CONSISTENCY 1.0

RUN apk add --update --no-cache openjdk8-jre && \
    gcloud --quiet components install cloud-datastore-emulator beta

EXPOSE $PORT

ENTRYPOINT gcloud --quiet beta emulators datastore start --no-store-on-disk --consistency $CONSISTENCY --host-port 0.0.0.0:$PORT
