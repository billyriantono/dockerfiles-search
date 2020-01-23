#Build Java project within gradle
FROM zenika/alpine-maven
ADD . ./
RUN cd ConfigurationService && mvn clean install -DskipTests
#Copy compiled java application and run within OpenJDK
FROM anapsix/alpine-java
RUN mkdir ./app/
COPY --from=0 /usr/src/app/ConfigurationService/target/release/ ./app/
WORKDIR ./app
ENV ENCRYPT_KEY=12345
CMD ["/opt/jdk/bin/java", "-jar", "ConfigurationService.jar"]
EXPOSE 8888
