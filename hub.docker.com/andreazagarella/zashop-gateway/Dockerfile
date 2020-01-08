ARG openjdkversion=8-jre-alpine

FROM maven:3-jdk-8 as mavenbuild
WORKDIR /root
ADD src  ./src
ADD pom.xml ./pom.xml
RUN mvn package -DskipTests

FROM openjdk:$openjdkversion
WORKDIR /root
COPY --from=mavenbuild /root/target/zashop-gateway-spring-boot.jar ./
EXPOSE 8762
CMD ["java", "-Djava.security.edg=file:/dev/./urandom","-Dproxy.eng.enable=false","-jar","zashop-gateway-spring-boot.jar"]

