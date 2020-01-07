from openjdk:11.0.4-jdk

RUN mkdir -p /app/build
RUN mkdir -p /app/run

ADD . /app/build/
WORKDIR /app/build
RUN ./mvnw clean install
RUN cp target/*.jar /app.jar
RUN rm -rf /app

VOLUME /input
VOLUME /output

WORKDIR /app/run/


ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]

