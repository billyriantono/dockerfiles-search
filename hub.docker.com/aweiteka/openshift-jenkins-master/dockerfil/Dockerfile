FROM debian:jessie

RUN apt-get clean && apt-get update && \
    apt-get install -y --fix-missing python python-dev python-pip && \
    apt-get install openvpn -y

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY entrypoint.sh entrypoint.sh

ENV OPENVPN_PASS_FILE pass
ENV OPENVPN_CONF_FILE client.ovpn

EXPOSE 1194
VOLUME /deployment
WORKDIR /deployment

ENTRYPOINT ["/entrypoint.sh"]
