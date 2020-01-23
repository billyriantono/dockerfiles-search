#Build Java project within gradle
FROM zenika/alpine-maven
ADD . ./
RUN cd DiscoveryService && mvn clean install -DskipTests
#Copy compiled java application and run within OpenJDK
FROM anapsix/alpine-java
RUN mkdir ./app/
COPY --from=0 /usr/src/app/DiscoveryService/target/release/ ./app/
WORKDIR ./app
CMD ["/opt/jdk/bin/java", "-jar", "DiscoveryService.jar"]
EXPOSE 8761
