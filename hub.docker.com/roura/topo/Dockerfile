FROM debian

ENV SERVICE serveo.net
ENV SERVICE_PORT 1337

COPY serveo /
COPY start /

RUN apt-get update && apt-get -y install openssh-client \
    && ssh-keygen -b 2048 -t rsa -f /serveo_key -q -N ""

RUN chmod +x /serveo /start

CMD ["sh", "start"]
