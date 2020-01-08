FROM openjdk:8-jdk-alpine

RUN apk add curl && curl -SL https://archive.apache.org/dist/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz | tar -zxC /home/

RUN ln -s /home/apache-hive-1.2.1-bin /home/hive
ADD https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.40/mysql-connector-java-5.1.40.jar /home/hive/lib/mysql-connector-java.jar

WORKDIR /home/hive/

ENTRYPOINT ["bin/hive"]
CMD ["--service", "metastore"]
