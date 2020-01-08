FROM openjdk:8-jre-alpine

ENV YOJIK_VERSION 0.0.2
ENV GPG_KEY D50F36ED104E13C1922580DDDD8A435D532E388E

RUN apk add --no-cache \
  gnupg

RUN set -eux; \
      gpg --keyserver ha.pool.sks-keyservers.net --recv-keys $GPG_KEY; \
      wget -O yojik.jar https://github.com/thomasylee/yojik/releases/download/v$YOJIK_VERSION/yojik-assembly-$YOJIK_VERSION.jar; \
      wget -O yojik.jar.sig https://github.com/thomasylee/yojik/releases/download/v$YOJIK_VERSION/yojik-assembly-$YOJIK_VERSION.jar.sig; \
      wget -O keystore.jks https://github.com/thomasylee/yojik/raw/v$YOJIK_VERSION/keystore.jks; \
      gpg --batch --verify yojik.jar.sig yojik.jar

EXPOSE 5222

CMD ["java", "-jar", "yojik.jar"]
