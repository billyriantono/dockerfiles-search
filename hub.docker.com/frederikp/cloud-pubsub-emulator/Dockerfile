FROM google/cloud-sdk:alpine

EXPOSE 8085

RUN apk --update add openjdk8-jre
RUN gcloud -q components install beta pubsub-emulator

ENTRYPOINT [ "gcloud", "beta", "emulators", "pubsub", "start" ]