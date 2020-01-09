FROM maven:3.3-jdk-8-onbuild

FROM openjdk:8u171-slim
COPY --from=0 /usr/src/app/target/app-thorntail.jar /opt/app.jar
#COPY target/app-thorntail.jar /opt/app.jar
CMD ["java","-XX:+UnlockExperimentalVMOptions","-XX:+UseCGroupMemoryLimitForHeap","-jar","/opt/app.jar","-Djava.net.preferIPv4Stack=true"]
