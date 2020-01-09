FROM adoptopenjdk:11-jre-hotspot

RUN  apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/*

# Add the flyway user and step in the directory
RUN adduser --system --home /flyway --disabled-password --group flyway
WORKDIR /flyway

# Change to the flyway user
USER flyway

ENV FLYWAY_VERSION 6.0.0-beta2

RUN curl -L https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/${FLYWAY_VERSION}/flyway-commandline-${FLYWAY_VERSION}.tar.gz -o flyway-commandline-${FLYWAY_VERSION}.tar.gz \
  && tar -xzf flyway-commandline-${FLYWAY_VERSION}.tar.gz --strip-components=1 \
  && rm flyway-commandline-${FLYWAY_VERSION}.tar.gz

RUN wget -P /flyway/sql https://kloudio-docker.s3-us-west-2.amazonaws.com/postgres/migrations/migrations.tar.gz
RUN tar -xvzf /flyway/sql/migrations.tar.gz --directory /flyway/sql/
RUN mv /flyway/sql/migrations/* /flyway/sql/
RUN rm -rf /flyway/sql/migrations
RUN rm /flyway/sql/migrations.tar.gz

ENTRYPOINT ["/flyway/flyway"]
CMD ["-?"]
