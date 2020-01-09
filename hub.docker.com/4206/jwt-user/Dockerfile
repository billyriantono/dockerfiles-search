#Build Java project within gradle
FROM zenika/alpine-maven
ADD . ./
RUN mvn clean install -DskipTests
#Copy compiled java application and run within OpenJDK
FROM anapsix/alpine-java
RUN mkdir ./app/
COPY --from=0 /usr/src/app/UserService/target/release/ ./app/
WORKDIR ./app
CMD ["/opt/jdk/bin/java", "-Xmx2048m", "-jar", "UserService.jar"]
EXPOSE 8082
