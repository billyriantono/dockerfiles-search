FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y curl zip wget nano gnupg \
    && curl -fsSL https://deb.nodesource.com/setup_8.x -o /tmp/node_setup.sh \
    && bash /tmp/node_setup.sh \
    && rm /tmp/node_setup.sh \
    && apt-get install -y nodejs git make g++ libboost-dev libboost-system-dev libboost-date-time-dev \
    && git clone https://github.com/MoneroOcean/xmr-node-proxy /xmr-node-proxy \
    && cd /xmr-node-proxy \
    && npm install \
    && cp -n config_example.json config.json \
    && openssl req -subj "/C=IT/ST=Pool/L=Daemon/O=Mining Pool/CN=mining.proxy" -newkey rsa:2048 -nodes -keyout cert.key -x509 -out cert.pem -days 36500

RUN chown -R proxy.proxy /xmr-node-proxy
RUN chmod 777 -R /xmr-node-proxy
