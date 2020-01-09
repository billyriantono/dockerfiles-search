FROM balenalib/raspberrypi3
ENV DEBIAN_FRONTEND noninteractive
RUN [ "cross-build-start" ]
RUN apt-get update && apt-get install -y git binutils unzip zip python
RUN apt-get update && apt-get install -y curl ca-certificates
RUN apt-get update && apt-get install -y build-essential libudev-dev pkg-config protobuf-compiler
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
RUN unzip awscli-bundle.zip
RUN ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
WORKDIR /home/piper/piper-builder
COPY . piper2
WORKDIR piper2
RUN [ "cross-build-end" ]
CMD [ "bash" ]
