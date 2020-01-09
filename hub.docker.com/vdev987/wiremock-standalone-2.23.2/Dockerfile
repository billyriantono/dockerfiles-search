FROM openjdk:8-jdk-alpine

ADD http://repo1.maven.org/maven2/com/github/tomakehurst/wiremock-standalone/2.23.2/wiremock-standalone-2.23.2.jar /apps/wiremock.jar

ENTRYPOINT ["java" ,"-jar", "/apps/wiremock.jar", "--https-port", "8443"]
CMD ["--global-response-templating"]