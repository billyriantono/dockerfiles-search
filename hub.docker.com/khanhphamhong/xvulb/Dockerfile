FROM alpine/git
WORKDIR /app
RUN git clone https://github.com/khanhphamhong/XVulB.git

FROM maven:3.5-jdk-8-alpine
WORKDIR /app
COPY --from=0 /app/XVulB /app
RUN mvn install

FROM java:8
WORKDIR /app
COPY --from=1 /app/target/XVulB-0.0.1-SNAPSHOT.jar /app
CMD ["java","-jar","/app/XVulB-0.0.1-SNAPSHOT.jar"]
