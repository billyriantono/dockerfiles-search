# Base JDK Image
FROM openjdk:8-jre-alpine

VOLUME /app

WORKDIR /app
ADD /app /app

EXPOSE 25565

# CMD ["ls"]
CMD ["java", "-Xmx1024M", "-Xms1024M", "-jar", "server.jar", "nogui"]