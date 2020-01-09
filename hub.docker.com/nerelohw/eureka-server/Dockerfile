FROM nerelohw/docker-openjdk:8-jre-alpine3.7
LABEL MAINTAINER="wholerencom@gmail.com"

##application.properties
#server.port=8761
#server.contextPath=/
#server.ssl.enabled=false


ADD app /app

EXPOSE 8080

CMD ["java","-jar","/app/eureka.jar"]
