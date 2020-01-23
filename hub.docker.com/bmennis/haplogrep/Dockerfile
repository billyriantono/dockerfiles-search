FROM ubuntu:18.04

RUN apt update && apt install -y openjdk-8-jdk wget; \
mkdir haplogrep; \
cd haplogrep; \
wget https://github.com/seppinho/haplogrep-cmd/releases/download/v2.1.20/haplogrep-2.1.20.jar; \
chmod +x haplogrep-2.1.20.jar; \
apt clean build-essential wget && apt -y  autoclean && apt -y autoremove
