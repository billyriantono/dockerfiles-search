FROM google/cloud-sdk:alpine

ENV CLOUDSDK_CORE_PROJECT="emulator" \
    FIRESTORE_PROJECT_ID="emulator"

RUN apk --no-cache --update add openjdk8-jre \
 && gcloud components install --quiet cloud-firestore-emulator beta \
 && mkdir -p /var/lib/datastore \
 && rm -fr /var/cache/apk/*

VOLUME /var/lib/firestore

CMD ["/google-cloud-sdk/bin/gcloud", "beta", "emulators", "firestore", "start", "--host-port=0.0.0.0:8081"]

