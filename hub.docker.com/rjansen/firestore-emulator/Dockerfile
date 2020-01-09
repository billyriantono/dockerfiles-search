FROM google/cloud-sdk:alpine

ARG PROJECT_ID=raizel

RUN apk add --update --no-cache openjdk8-jre &&\
    gcloud components install cloud-firestore-emulator beta --quiet

VOLUME /opt/data

EXPOSE 8086

RUN gcloud config set project $PROJECT_ID

ENTRYPOINT ["gcloud", "beta", "emulators", "firestore", "start", "--host-port=0.0.0.0:8086"]
