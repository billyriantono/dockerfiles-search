FROM java:8-jdk-alpine

COPY ./tourofheroes-api/target/tourofheroes-api.jar /usr/app/

WORKDIR /usr/app

RUN sh -c 'touch tourofheroes-api.jar'

ENTRYPOINT ["java","-jar","tourofheroes-api.jar"]
