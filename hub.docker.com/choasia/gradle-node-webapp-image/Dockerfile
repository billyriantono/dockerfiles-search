FROM gradle:5.5.1-jdk11

ENV DEBIAN_FRONTEND noninteractive

RUN apt update \
  && apt install -y docker.io \
  && apt install -y python3-pip \
  && apt install -y jq \
  && pip3 install --no-input docker-compose

RUN apt update \
  && apt install -y nodejs npm \
  && npm install n -g \
  && n 10.15.1 \
  && apt install -y mysql-client netcat sudo \
  && wget -qO- https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/6.0.3/flyway-commandline-6.0.3-linux-x64.tar.gz | tar xvz && sudo ln -s `pwd`/flyway-6.0.3/flyway /usr/local/bin

ENTRYPOINT ["/bin/bash", "--login"]
