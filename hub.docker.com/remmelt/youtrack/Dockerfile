FROM java:8-jre
MAINTAINER Remmelt Pit <remmelt@remmelt.com>

ENV DEBIAN_FRONTEND noninteractive

ENV YOUTRACK_VERSION 6.0.12463

RUN mkdir -p /youtrack /youtrack-data
RUN wget -nv http://download.jetbrains.com/charisma/youtrack-$YOUTRACK_VERSION.jar -O /youtrack/youtrack-$YOUTRACK_VERSION.jar
RUN ln -s /youtrack/youtrack-$YOUTRACK_VERSION.jar /youtrack/youtrack.jar

COPY log4j.xml /youtrack/

EXPOSE 8080

VOLUME /youtrack-data

CMD ["java", \
  "-Xmx1g", \
  "-Duser.home=/youtrack", \
  "-Ddatabase.location=/youtrack-data", \
  "-Ddatabase.backup.location=/youtrack-data", \
  "-Djavax.net.ssl.trustStore=/etc/ssl/certs/java/cacerts", \
  "-Djavax.net.ssl.trustStorePassword=changeit", \
  "-Djetbrains.youtrack.disableBrowser=true", \
  "-Djetbrains.youtrack.enableGuest=false", \
  "-Djetbrains.mps.webr.log4jPath=/youtrack/log4j.xml", \
  "-Djava.awt.headless=true", \
  "-jar", \
  "/youtrack/youtrack.jar", \
  "8080"]
