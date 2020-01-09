# teambitflow/anomaly-detection
FROM maven:3.6-jdk-11 as build
WORKDIR /build
COPY . .
RUN mvn install && \
    mkdir -p compiled/algorithms && \
    cp pom.xml compiled/ && \
    cp algorithms/target/IFTM-anomalydetection-models-*.jar compiled/algorithms/anomaly-detection.jar && \
    cp algorithms/pom.xml compiled/algorithms/

FROM alpine:3.9
COPY --from=build /build/compiled/ anomaly-detection/
