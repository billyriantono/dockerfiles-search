FROM alpine
RUN apk -v add --no-cache \
        ca-certificates \
        python \
        py-pip && \
    pip install --upgrade awscli && \
    apk -v --purge del py-pip
RUN wget -O /usr/local/bin/ecs-cli https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-amd64-latest && chmod +x /usr/local/bin/ecs-cli
RUN adduser -D aws
USER aws
WORKDIR /home/aws

# Enable saving profiles in ~/.ecs
ENV HOME=/home/aws
