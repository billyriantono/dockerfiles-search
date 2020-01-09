FROM openjdk:8-jdk-alpine
VOLUME /tmp
VOLUME /home/mirth
ADD data-generator-0.0.1-SNAPSHOT.jar app.jar
COPY HL7s /home/mirth/HL7s
COPY FHIRs /home/mirth/FHIRs
EXPOSE 8888
ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]
