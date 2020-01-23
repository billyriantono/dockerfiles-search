FROM docker.io/ubuntu:latest
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y unzip
RUN mkdir -p /mindoc
WORKDIR /mindoc
RUN wget https://github.com/lifei6671/mindoc/releases/download/v2.0-beta.2/mindoc_linux_amd64.zip
RUN unzip mindoc_linux_amd64.zip
RUN /mindoc/mindoc_linux_amd64 install
RUN ln -s /mindoc/mindoc_linux_amd64 /usr/bin/mindoc_linux_amd64
RUN apt-get clean

EXPOSE 8181 8181
ENTRYPOINT ["mindoc_linux_amd64"]
