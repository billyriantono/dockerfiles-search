FROM homecentral/base:feature-poc

ADD init.py /init.py
ADD entrypoint.sh /entrypoint.sh
ADD config-schema.json /config-schema.json
ADD config-template.j2 /config-template.j2

RUN apk add --no-cache aria2 && \
    chmod +x /entrypoint.sh

WORKDIR /webui

# Aria2 RPC
EXPOSE 6800

ENTRYPOINT [ "/bin/ash", "/entrypoint.sh" ]