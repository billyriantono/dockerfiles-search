FROM ubuntu:xenial

RUN apt-get update && apt-get install -y \
    ca-certificates \
    wget \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /wolfram

ADD http://account.wolfram.com/download/public/wolfram-engine/desktop/LINUX WolframEngine_12.0.0_LINUX.sh

RUN chmod +x WolframEngine_12.0.0_LINUX.sh

RUN ./WolframEngine_12.0.0_LINUX.sh

RUN rm WolframEngine_12.0.0_LINUX.sh

CMD ["wolframscript"]
