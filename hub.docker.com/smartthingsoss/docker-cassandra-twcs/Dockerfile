FROM cassandra:2.1.15
MAINTAINER SmartThings OSS <smartthingsoss@docker.com>
LABEL Description="Cassandra 2.1.15 with TimeWindowCompactionStrategy jar on the classpath"

ENV CLASSPATH "/opt/TimeWindowCompactionStrategy-JDK7-2.1.13.jar"
ADD ./TimeWindowCompactionStrategy-JDK7-2.1.13.jar /opt/TimeWindowCompactionStrategy-JDK7-2.1.13.jar
