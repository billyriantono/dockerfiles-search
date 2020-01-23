FROM maven:3-jdk-8

ENV PARAMS=""

RUN wget https://codeload.github.com/xuxueli/xxl-conf/zip/master
RUN mkdir /source
RUN unzip master -d /source
WORKDIR /source/xxl-conf-master
RUN mvn clean package -Dmaven.test.skip=true

FROM openjdk:8-jre
LABEL maintainer="conf"
COPY --from=0 /source/xxl-conf-master/xxl-conf-admin/target/xxl-conf-admin-*.jar /app.jar
ENTRYPOINT ["sh","-c","java -jar /app.jar $PARAMS"]
EXPOSE 8080
