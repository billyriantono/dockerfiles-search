FROM nerelohw/docker-openjdk:8-jre-alpine3.7
LABEL MAINTAINER="wholerencom@gmail.com"

##application.properties
#server.port=8080
#server.contextPath=/
#server.ssl.enabled=false

#spring.boot.admin.username=root
#spring.boot.admin.password=bootadmin


ADD app /app

EXPOSE 8080

CMD ["java","-jar","/app/bootadmin.war"]