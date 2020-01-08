# Version: 0.0.1
FROM farberg/hadoop-docker:latest
MAINTAINER Andy C "aecobley@dundee.ac.uk", now Dennis Pfisterer (https://github.com/pfisterer/)

RUN curl http://apache.mirror.anlx.net/pig/latest/pig-0.17.0.tar.gz | tar -zx -C /usr/local
ENV PATH /usr/local/pig-0.17.0/bin:$PATH

RUN curl http://apache.mirror.anlx.net/hive/stable/apache-hive-1.2.2-bin.tar.gz | tar -zx -C /usr/local
ENV PATH /usr/local/apache-hive-1.2.2-bin/bin:$PATH

ENV JAVA_HOME /usr/lib/jvm/jre-1.8.0-openjdk.x86_64/bin/java

EXPOSE 10020
EXPOSE 50070
EXPOSE 50030
EXPOSE 8088
