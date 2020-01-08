FROM alpine:3.10.1

RUN apk update; \
    apk upgrade; \
    apk add openjdk11-jre=11.0.4_p4-r1

EXPOSE 8080/tcp 8082/tcp 443/tcp 8443/tcp

CMD ["java", "-version"]