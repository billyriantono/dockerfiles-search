FROM java:alpine
EXPOSE 9324

RUN apk add --update curl && \
    rm -rf /var/cache/apk/*


ENV VERSION 0.13.2

RUN curl -o elasticmq-server.jar https://s3-eu-west-1.amazonaws.com/softwaremill-public/elasticmq-server-${VERSION}.jar

ADD configuration.conf configuration.conf

CMD ["java", "-Dconfig.file=configuration.conf", "-jar", "elasticmq-server.jar"]
