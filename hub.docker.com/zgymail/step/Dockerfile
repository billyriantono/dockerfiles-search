FROM registry.cn-hangzhou.aliyuncs.com/zgy/step
MAINTAINER zgy
VOLUME /tmp
VOLUME /root/.m2
RUN ls /root/.m2
ADD ./src/main/proto/protoc3.1/linux/protoc  /usr/local/bin/
ADD ./ /app
WORKDIR /app/

RUN /usr/local/bin/protoc --version
RUN mvn package 
CMD ["java", "-Xmx200m", "-jar", "target/step-server-1.0.jar"]
EXPOSE 8443