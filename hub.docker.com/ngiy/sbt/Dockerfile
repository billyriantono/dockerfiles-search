FROM java:8-alpine
MAINTAINER ngiy

RUN apk update
RUN apk add ca-certificates wget bash openssh git python py-pip docker jq curl
RUN update-ca-certificates
RUN wget -O - https://github.com/sbt/sbt/releases/download/v1.1.0/sbt-1.1.0.tgz | gunzip | tar -x -C /usr/local
RUN pip install awscli
RUN wget -P /usr/bin/ https://raw.githubusercontent.com/silinternational/ecs-deploy/master/ecs-deploy
RUN chmod +x /usr/bin/ecs-deploy
ENV PATH="/usr/local/sbt/bin:${PATH}"