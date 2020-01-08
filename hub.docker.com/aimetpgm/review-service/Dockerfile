FROM frolvlad/alpine-oraclejdk8:slim
VOLUME /tmp
ADD ./target/review-service-0.0.1.jar review-service.jar
RUN sh -c 'touch /review-service.jar'
ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /review-service.jar" ]