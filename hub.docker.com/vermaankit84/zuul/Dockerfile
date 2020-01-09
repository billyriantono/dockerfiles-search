FROM openjdk:8
VOLUME /tmp
ADD target/zuul-0.0.1-SNAPSHOT.jar zuul-0.0.1-SNAPSHOT.jar
EXPOSE 8090
ENTRYPOINT [ "java" , "-jar" , "zuul-0.0.1-SNAPSHOT.jar" ]