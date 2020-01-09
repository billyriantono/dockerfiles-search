FROM openjdk:8-jdk

RUN \
    apt-get update && \
    apt-get install -y jq python-pip && \
    export FLYWAY_VERSION=5.1.4 && \
    curl -L https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/${FLYWAY_VERSION}/flyway-commandline-${FLYWAY_VERSION}.tar.gz -o flyway-commandline-${FLYWAY_VERSION}.tar.gz && \
    tar -xzf flyway-commandline-${FLYWAY_VERSION}.tar.gz --strip-components=1 && \
    rm flyway-commandline-${FLYWAY_VERSION}.tar.gz && \
    pip install awscli --user --upgrade && \
    echo 'export PATH=~/.local/bin:$PATH' >> ~/.profile && \
    ln -s /flyway/flyway /usr/local/bin/flyway