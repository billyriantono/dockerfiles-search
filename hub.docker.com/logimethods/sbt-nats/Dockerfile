FROM hseeberger/scala-sbt

RUN cd / \
    && wget https://github.com/nats-io/gnatsd/releases/download/v1.3.0/gnatsd-v1.3.0-linux-amd64.zip -O gnatsd.zip \
    && unzip gnatsd.zip \
    && rm gnatsd.zip

ENV PATH $PATH:/gnatsd-v1.3.0-linux-amd64

RUN cd / \
    && wget https://github.com/nats-io/nats-streaming-server/releases/download/v0.11.2/nats-streaming-server-v0.11.2-linux-amd64.zip -O nats-streaming-server.zip\
    && unzip nats-streaming-server.zip \
    && rm nats-streaming-server.zip
    
ENV PATH $PATH:/nats-streaming-server-v0.11.2-linux-amd64
