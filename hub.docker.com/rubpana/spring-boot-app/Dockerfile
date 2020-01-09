FROM java:8
LABEL maintainer="Rubén Panadero"
VOLUME /data
EXPOSE 8080

ENV SPRING_BOOT_APP_JAR /data/target/*.jar

CMD java -jar $SPRING_BOOT_APP_JAR
