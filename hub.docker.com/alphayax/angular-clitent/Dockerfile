FROM openjdk:8

ENV SBT_VERSION 1.2.8

RUN apt-get update && \
    apt-get install -y scala python-pip

# Install sbt
RUN \
  curl -L -o sbt-$SBT_VERSION.deb http://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install -y sbt && \
  sbt sbtVersion

RUN pip install awscli && \
    curl -o /usr/local/bin/ecs-cli https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-amd64-latest && \
    chmod +x /usr/local/bin/ecs-cli

# Define working directory
WORKDIR /root