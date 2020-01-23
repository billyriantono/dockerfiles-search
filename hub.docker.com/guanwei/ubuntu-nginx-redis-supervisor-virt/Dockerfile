ARG COMMIT=48d8a888554f0fbee6aeaf2a4f79ebb34ea49c33
FROM maven:3-jdk-8 as build

ARG COMMIT
ENV COMMIT ${COMMIT}
ADD https://github.com/malyvoj3/csvw-validator/archive/${COMMIT}.zip /tmp/
RUN \
  unzip /tmp/${COMMIT}.zip -d /usr/src/ && \
  cd /usr/src/csvw-validator-${COMMIT} && \
  mvn install

FROM openjdk:8-alpine
ARG COMMIT
ENV COMMIT ${COMMIT}
COPY --from=build /usr/src/csvw-validator-${COMMIT}/csvw-validator-cli-app/target/csvw-validator-cli-app-1.0.0-SNAPSHOT.jar /usr/local/lib/validator.jar
CMD java -jar /usr/local/lib/validator.jar
