FROM maven:3.3-jdk-8-onbuild

CMD ["java","-jar","/usr/src/app/game-of-life/target/gameoflife-build-1.0-SNAPSHOT.jar"]

RUN mkdir /opt/gameoflife

# development script to stop the app, redeploy the jar and restart

# application and startup script
ADD /usr/src/app/gameoflife-web/target/gameoflife-build-1.0-SNAPSHOT.jar /usr/local/gameoflife-build-1.0-SNAPSHOT.jar


