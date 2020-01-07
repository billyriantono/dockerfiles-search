 FROM openjdk:8u131-jre-alpine
  MAINTAINER <Huangzy>
  USER root
  ENV LANG=C.UTF-8
  RUN apk add --no-cache  --update-cache bash
  ENV TZ=Asia/Shanghai
  RUN apk --update add wget bash tzdata \
      && cp /usr/share/zoneinfo/$TZ /etc/localtime \
      && echo $TZ > /etc/timezone
      
  WORKDIR /usr/local
  RUN wget "http://www.apache.org/dist/spark/spark-2.0.2/spark-2.0.2-bin-hadoop2.7.tgz" \
     && tar -zxvf spark-*  \
     && mv spark-2.0.2-bin-hadoop2.7 spark \
     && rm -rf spark-2.0.2-bin-hadoop2.7.tgz

  ENV SPARK_HOME=/usr/local/spark
  ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
  ENV PATH=${PATH}:${JAVA_HOME}/bin:${SPARK_HOME}/bin

  EXPOSE 6066 7077 8080 8081 4044
  WORKDIR $SPARK_HOME
  CMD ["/bin/bash"]
