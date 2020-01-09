FROM alpine/git
WORKDIR /assignment10
RUN git clone https://github.com/denisdbell/spring-petclinic.git

FROM maven:3.5-jdk-8-alpine
WORKDIR /assignment10
COPY --from=0 /assignment10/spring-petclinic /assignment10 
RUN mvn clean package -DskipTests

FROM openjdk:8-jre-alpine
WORKDIR /assignment10
VOLUME /assignment10/log
COPY --from=1 /assignment10/target/*.jar .
CMD java -jar *.jar 

EXPOSE 8080