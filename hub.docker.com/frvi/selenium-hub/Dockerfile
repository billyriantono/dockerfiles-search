FROM java:7

MAINTAINER Fredrik Vihlborg <fredrik.wihlborg@gmail.com>

RUN wget -P /opt http://selenium-release.storage.googleapis.com/2.43/selenium-server-standalone-2.43.1.jar

EXPOSE 4444

ENTRYPOINT ["java", "-jar", "/opt/selenium-server-standalone-2.43.1.jar", "-role", "hub"]
