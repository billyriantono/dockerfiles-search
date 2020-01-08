FROM openjdk:8u151-jre-alpine

RUN mkdir /gitbucket && ln -s /gitbucket /root/.gitbucket
ADD https://github.com/sd-yip/Resilient-GitBucket/releases/download/4.21.2/gitbucket.war /opt/

WORKDIR /gitbucket
ENTRYPOINT ["java", "-jar", "/opt/gitbucket.war"]
