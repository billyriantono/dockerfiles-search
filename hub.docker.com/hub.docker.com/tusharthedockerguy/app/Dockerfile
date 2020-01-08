FROM alpine:edge
RUN apk add openjdk8
COPY /target/app.jar /opt/
ENTRYPOINT ["/usr/bin/java"]
CMD ["-jar", "/opt/app.jar"]
EXPOSE 8123

