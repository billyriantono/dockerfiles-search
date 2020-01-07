FROM google/cloud-sdk:206.0.0-alpine

RUN apk --update add openjdk7-jre
RUN gcloud components install bigtable bq cbt cloud-datastore-emulator datalab pubsub-emulator
