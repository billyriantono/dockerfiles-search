FROM ubuntu
MAINTAINER ming <liumingmad@gmail.com>
EXPOSE 8001
COPY . /app
WORKDIR /app
RUN apt update && apt install -y \
    gnugo \
    unzip \
    wget

RUN wget https://github.com/joewalnes/websocketd/releases/download/v0.3.0/websocketd-0.3.0-linux_amd64.zip -O ws.zip
RUN unzip -n ws.zip
CMD ["/bin/bash", "/app/start.sh"]
