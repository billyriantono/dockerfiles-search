FROM java:8-jre
MAINTAINER Erlend Klakegg Bergheim

EXPOSE 8080

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre/
ENV VERSION 2.0-beta.2.2
ENV PMODES /holodeck-b2b/examples/pmodes/ex-pm-push-resp.xml

ADD . /build
RUN /build/build.sh

VOLUME /holodeck-b2b/data

CMD /build/run.sh
