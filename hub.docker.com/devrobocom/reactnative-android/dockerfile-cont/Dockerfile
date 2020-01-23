#
# Image for Open DevOps Pipeline
#
#VERSION : 0.1
FROM docker.io/java:openjdk-8-jdk

#Maintainer
MAINTAINER Open DevOps Team <open.devops@gmail.com>

RUN \
  mkdir /hygieia

COPY *.jar /hygieia/
COPY k8s-properties-builder.sh /hygieia/

WORKDIR /hygieia

VOLUME ["/hygieia/logs"]

CMD ./k8s-properties-builder.sh && \
  java -jar kubernetes-deployment-collector*.jar --spring.config.location=/hygieia/hygieia-k8s-collector.properties
