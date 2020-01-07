FROM library/openjdk:8-jdk-alpine

RUN apk add --update --no-cache bash shadow git openssh-client docker maven && \
    useradd -d /home/jenkins -G docker jenkins && \
    mkdir -p /home/jenkins && \
    chown jenkins /home/jenkins

CMD "dockerd"
