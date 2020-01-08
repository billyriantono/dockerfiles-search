FROM google/cloud-sdk:latest

ENV GOOGLE_PROJECT fake-project
ENV DATASTORE_CONSISTENCY 0.9

EXPOSE 8081

CMD ["/bin/sh", "-c", "gcloud config set project $GOOGLE_PROJECT && gcloud beta emulators datastore start --no-store-on-disk --host-port=0.0.0.0:8081 --consistency=$DATASTORE_CONSISTENCY"]
