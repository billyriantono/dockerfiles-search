FROM openjdk:8
  
ADD http://archive.apache.org/dist/qpid/java/6.0.4/binaries/qpid-broker-6.0.4-bin.tar.gz /opt

WORKDIR /opt

RUN tar zxf qpid-broker-6.0.4-bin.tar.gz && rm qpid-broker-6.0.4-bin.tar.gz

EXPOSE 5672 8080

CMD /opt/qpid-broker/6.0.4/bin/qpid-server