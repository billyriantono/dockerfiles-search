# docker build -t yuanying/curl:v0.1.0 .
# docker run yuanying/curl

FROM debian:wheezy-slim
MAINTAINER OTSUKA, Yuanying "yuan-docker@fraction.jp"

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean

CMD ["bash"]
