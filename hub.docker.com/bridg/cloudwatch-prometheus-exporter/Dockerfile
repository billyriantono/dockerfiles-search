FROM openjdk:8-jre-alpine

RUN apk update \
 && apk --no-cache add ca-certificates openssl git \
 && update-ca-certificates

ENV DOCKERIZE_VERSION v0.3.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
 && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
 && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

COPY cloudwatch_exporter-0.5-SNAPSHOT-jar-with-dependencies.jar /cloudwatch_exporter/cloudwatch_exporter.jar
COPY ./templates/config.tmpl /cloudwatch_exporter/config.tmpl

ENTRYPOINT ["dockerize", "-template", "/cloudwatch_exporter/config.tmpl:/cloudwatch_exporter/config.yml"]
CMD ["java", "-jar", "/cloudwatch_exporter/cloudwatch_exporter.jar", "9106", "/cloudwatch_exporter/config.yml"]
