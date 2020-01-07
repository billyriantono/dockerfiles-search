FROM google/cloud-sdk:alpine
RUN apk --update --no-cache add openjdk8-jre git mercurial make musl-dev go
RUN gcloud components install cloud-datastore-emulator beta
