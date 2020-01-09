FROM alpine/git
WORKDIR /app
RUN git clone https://github.com/JeffreyBrettColeman/rxp2p-tracker.git

FROM maven:3.5-jdk-8-alpine
WORKDIR /app
COPY --from=0 /app/rxp2p-tracker /app 
RUN mvn install package


FROM openjdk:8-jdk-alpine
WORKDIR /app
COPY --from=1 /app/ /app/
RUN ls -la /app/target
VOLUME /tmp
ENTRYPOINT ["java","-jar","/app/target/rxp2p-tracker-0.0.1-SNAPSHOT.jar"]