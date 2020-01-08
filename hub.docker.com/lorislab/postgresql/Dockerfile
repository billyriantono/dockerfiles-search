FROM maven:3.6.0-jdk-11 as build

COPY . /build

RUN cd build && mvn clean package

FROM scratch

COPY --from=build /build/target/release /opt/postgresql


