FROM debian:latest
RUN mkdir /app
ENV NODEJS_VERSION 0.10.35
RUN apt-get update && apt-get upgrade -y && apt-get install -y git curl tar gzip && rm -rf /var/lib/apt/lists/*
RUN curl http://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.gz | \
    tar xzv -C /tmp/ && mv /tmp/node-* /node
ENV PATH /node/bin:$PATH
WORKDIR /app
ENTRYPOINT ["npm"]
CMD ["start"]
