FROM ubuntu

RUN apt update && apt install -y dnsutils curl telnet wget
RUN wget https://github.com/jmespath/jp/releases/download/0.1.2/jp-linux-amd64 -O /usr/local/bin/jp \
&& chmod +x /usr/local/bin/jp

