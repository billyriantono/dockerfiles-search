FROM frekele/ant AS build

WORKDIR /build

RUN \
apt update && \
apt install -y git && \
git clone https://github.com/laurent-clouet/sheepit-client.git && \
cd sheepit-client && \
git checkout proxy && \
ant && \
find .

FROM alpine:3.8

WORKDIR /app

COPY --from=build /build/sheepit-client/bin/sheepit-proxy.jar sheepit-proxy.jar

RUN apk --update add openjdk8-jre

CMD ["java", "-jar", "sheepit-proxy.jar", "-ui", "text"]

EXPOSE 2060
