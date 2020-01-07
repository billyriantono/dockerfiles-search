FROM maven:3-jdk-8
COPY . /tmp/app
COPY build.sh /
RUN /build.sh
ENTRYPOINT java -jar /tmp/app/target/gs-spring-boot-0.1.0.jar