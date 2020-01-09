FROM openjdk:12-jdk-alpine as build
RUN rm -rf $JAVA_HOME/jmods; rm -f $JAVA_HOME/lib/src.zip

FROM alpine:3.9

ENV JAVA_HOME /opt/openjdk-12
ENV PATH $JAVA_HOME/bin:$PATH

COPY --from=build $JAVA_HOME $JAVA_HOME
ENV JAVA_VERSION=12-ea+29

CMD ["jshell"]
