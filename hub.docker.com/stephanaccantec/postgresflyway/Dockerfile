FROM openjdk:8-jre

ENV FLYWAY_VERSION 5.1.4

WORKDIR /flyway

RUN curl -L https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/${FLYWAY_VERSION}/flyway-commandline-${FLYWAY_VERSION}.tar.gz -o flyway-commandline-${FLYWAY_VERSION}.tar.gz \
  && tar -xzf flyway-commandline-${FLYWAY_VERSION}.tar.gz --strip-components=1 \
  && rm flyway-commandline-${FLYWAY_VERSION}.tar.gz \
  && ln -s /flyway/flyway /usr/local/bin/flyway

RUN chgrp -R 0  /usr/local/bin/flyway && \
    chmod -R g=u /usr/local/bin/flyway

#RUN useradd -ms /bin/bash flywayuser

USER 1000

ENTRYPOINT ["flyway"]
CMD ["-?"]
