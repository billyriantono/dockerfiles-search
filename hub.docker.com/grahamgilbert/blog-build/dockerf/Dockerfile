FROM gracig/devops-builder:alpine3.4-jdk1.8-mvn3.3.9-1
MAINTAINER gracig <gerson.graciani@gmail.com>

ADD  .  /src/
WORKDIR /src 

CMD ["mvn", "test"]
