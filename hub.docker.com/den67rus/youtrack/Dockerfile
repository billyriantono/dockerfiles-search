FROM java:8
MAINTAINER Maarten Balliauw <maarten.balliauw@jetbrains.com>

RUN wget https://download.jetbrains.com/charisma/youtrack-2017.3.37328.jar -O youtrack.jar

EXPOSE 80
CMD ["java", "-Djava.security.egd=/dev/zrandom", "-Xmx1g", "-XX:MaxPermSize=250m", "-Djava.awt.headless=true", "-jar", "youtrack.jar", "80"]
