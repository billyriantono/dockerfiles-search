FROM karalabe/xgo-1.8.x

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y zip git curl

ENV GOBIN=/usr/local/go/bin
ENV PATH=$PATH:/usr/local/go/bin
RUN curl https://glide.sh/get | sh

