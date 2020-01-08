FROM debian:buster
RUN apt-get update && apt-get upgrade -y && apt-get install -y rclone ca-certificates
RUN adduser --disabled-password --gecos Vainu vainu
WORKDIR /opt
USER vainu:vainu
