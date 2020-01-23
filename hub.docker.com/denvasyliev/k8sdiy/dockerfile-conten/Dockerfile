FROM ubuntu:16.04
MAINTAINER Denley Hsiao <denley@justtodo.com>

ENV APP_DIR /root/app
RUN mkdir -p $APP_DIR
COPY . $APP_DIR

WORKDIR $APP_DIR
SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install lib32z1 -y \
 && dpkg -i driver/aksusbd_7.80-1_amd64.deb

CMD ["./startup.sh"]
