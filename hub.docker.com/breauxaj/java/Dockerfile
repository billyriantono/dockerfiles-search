FROM breauxaj/alpine:latest

RUN apk add openjdk11-jdk \
  apache-ant \
  maven \
  && rm -rf /var/cache/apk/*

RUN cd /usr/bin \
  && ln -s ../lib/jvm/default-jvm/jre/bin/javac . \
  && ln -s ../lib/jvm/default-jvm/jre/bin/jar . 

CMD ["sh"]

LABEL org.opencontainers.image.vendor="Breaux Heavy Industries" \
	org.opencontainers.image.url="https://breaux.io" \
	org.opencontainers.image.title="OpenJDK" \
	org.opencontainers.image.description="OpenJDK 11 installation with Ant and Maven" \
	org.opencontainers.image.version="v0.0.1" \
	org.opencontainers.image.documentation="https://docs.breaux.io"