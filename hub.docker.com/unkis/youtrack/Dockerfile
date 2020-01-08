FROM java:8-jre
MAINTAINER Yuriy Barvenko <yuriy.barvenko@gmail.com>

RUN wget http://download-cf.jetbrains.com/charisma/youtrack-6.5.16433.jar -O youtrack.jar

EXPOSE 80
CMD ["java", "-Xmx1g", "-XX:MaxMetaspaceSize=250m", "-Djavax.net.ssl.trustStore=/etc/ssl/certs/java/cacerts", "-Djavax.net.ssl.trustStorePassword=changeit", "-Djava.awt.headless=true", "-Djetbrains.youtrack.disableBrowser=true", "-Djetbrains.youtrack.disableCheckForUpdate=true", "-jar", "youtrack.jar", "80"]
