FROM maven:3.5-jdk-8-alpine

RUN addgroup -g 1000 -S user \
 && adduser -u 1000 -G user -S user \
 && mkdir -p /home/user/.m2/repository /cache \
 && chown -R user:user /home/user/ /cache

ENV MAVEN_CONFIG /home/user/.m2

USER user