FROM openjdk:8-jdk

COPY assets /minecraft
WORKDIR /minecraft

CMD java -Xmx3G -Xms3G -Dfml.queryResult=confirm -jar forge-1.12.2-14.23.5.2768-universal.jar nogui
