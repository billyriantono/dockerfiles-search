FROM openjdk:13-slim as build
WORKDIR /app
COPY . .
RUN ./gradlew -Dheadless=true -DskipDeleteTempPackageFiles=true buildPackage

FROM openjdk:13-slim
WORKDIR /app
COPY --from=build /app/dist/tmp/burst.jar .
COPY --from=build /app/html html
VOLUME ["/conf", "/db"]
COPY conf/brs.properties.h2 /conf/brs.properties
COPY conf/brs-default.properties /conf/brs-default.properties
COPY conf/logging-default.properties /conf/logging-default.properties
EXPOSE 8125 8123 8121
ENTRYPOINT ["java", "-jar", "burst.jar", "--config", "/conf"]
