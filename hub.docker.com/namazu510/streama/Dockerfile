FROM java:8-jre

ADD https://github.com/dularion/streama/releases/download/v1.1/streama-1.1.war /data/streama/streama.war
ADD application.yml /data/streama

WORKDIR /data/streama
CMD ["java", "-jar", "streama.war" ]
