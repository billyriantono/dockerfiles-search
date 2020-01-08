FROM java:openjdk-8-alpine

COPY elasticmq-server-0.13.8.jar /
COPY custom.conf /
ENTRYPOINT ["/usr/bin/java", "-Dconfig.file=custom.conf", "-jar", "/elasticmq-server-0.13.8.jar"]

EXPOSE 9324

CMD ["-help"]
