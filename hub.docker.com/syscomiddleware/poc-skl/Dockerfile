# COMPILE
FROM java:openjdk-8-alpine as compile
COPY . /home/source/java
WORKDIR /home/source/java
RUN ./gradlew clean build

# RUNTIME
FROM java:8-jre-alpine
WORKDIR /home/application/java
COPY --from="compile" "/home/source/java/build/libs/poc-skl.jar" .
#EXPOSE 8080
ENTRYPOINT [ "java", "-jar", "/home/application/java/poc-skl.jar"]
