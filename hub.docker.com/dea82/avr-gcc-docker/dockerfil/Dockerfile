# Stage 1 (Build)
FROM maven:3.3-jdk-8 as geo-builder

WORKDIR /usr/src/geo

COPY . .

RUN mvn package -DskipTests

# Stage 2 (Deploy)
FROM openjdk:8

WORKDIR /opt

RUN mkdir config

COPY --from=geo-builder /usr/src/geo/geo-core/target/geo-core.jar /opt/geo-service.jar

ADD ./config ./config

CMD ["/opt/geo-service.jar"]