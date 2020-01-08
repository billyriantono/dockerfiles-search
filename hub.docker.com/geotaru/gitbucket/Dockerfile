FROM openjdk:8-jre

MAINTAINER CoffeeTaro

RUN apt-get update -y && apt-get upgrade -y

ADD https://github.com/gitbucket/gitbucket/releases/download/4.22.0/gitbucket.war /opt/gitbucket.war
RUN ln -s /gitbucket /root/.gitbucket
VOLUME /gitbucket

EXPOSE 8080

CMD ["java", "-jar", "/opt/gitbucket.war"]
