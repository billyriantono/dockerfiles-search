FROM java:8
LABEL maintainer="Carlos Perez <carlosperezurena@gmail.com>"
VOLUME /tmp
EXPOSE 8082
ADD shop-0.0.1-SNAPSHOT.jar shop-0.0.1-SNAPSHOT.jar
ENTRYPOINT ["java", "-jar", "shop-0.0.1-SNAPSHOT.jar"]