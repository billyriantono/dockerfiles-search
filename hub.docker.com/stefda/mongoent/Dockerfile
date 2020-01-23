FROM java:8

COPY Dropwizard1-0.0.1-SNAPSHOT.jar .

COPY hello-world.yaml .

COPY pom.xml .

EXPOSE 8080

CMD ["java","-jar","Dropwizard1-0.0.1-SNAPSHOT.jar","server","hello-world.yaml"]
