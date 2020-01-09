FROM openjdk:8
MAINTAINER Philippe Le Van <philippe.levan@kibatic.com>

ENV YOUTRACK_VERSION=2017.2.34480

RUN wget http://download-cf.jetbrains.com/charisma/youtrack-$YOUTRACK_VERSION.jar -O youtrack.jar

EXPOSE 80

CMD ["java", "-Xmx1g", "-XX:MaxPermSize=250m", "-Djava.awt.headless=true", "-jar", "youtrack.jar", "80"]
