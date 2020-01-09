FROM debian:latest

RUN apt-get update && apt-get install wget -y

ENV VERSION=0.15.0

RUN wget "https://github.com/badaix/snapcast/releases/download/v${VERSION}/snapclient_${VERSION}_amd64.deb"

RUN dpkg -i --force-all snapclient_${VERSION}_amd64.deb
RUN apt-get -f install -y

ENTRYPOINT ["snapclient"]
