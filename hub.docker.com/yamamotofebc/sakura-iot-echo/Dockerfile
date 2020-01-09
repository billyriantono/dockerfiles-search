FROM alpine:3.4
LABEL maintainer="Kazumichi Yamamoto <yamamoto.febc@gmail.com>"
MAINTAINER Kazumichi Yamamoto <yamamoto.febc@gmail.com>

ADD https://github.com/yamamoto-febc/sakura-iot-go/releases/download/v0.0.3-alpha/sakura-iot-echo-server_linux-amd64.zip ./
RUN unzip sakura-iot-echo-server_linux-amd64.zip -d /bin; rm -f sakura-iot-echo-server_linux-amd64.zip

ENTRYPOINT ["/bin/sakura-iot-echo-server"]

