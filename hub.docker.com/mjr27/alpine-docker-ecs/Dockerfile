FROM docker:latest

ADD https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest /bin/ecs-cli
ADD ca-certificates.crt /etc/ssl/certs/
RUN chmod 755 /bin/ecs-cli && \
    apk add --update --no-cache python python-dev py-pip && \
    pip install --upgrade --no-cache-dir awscli
