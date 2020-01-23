# https://github.com/macropin/docker-sshd/blob/master/Dockerfile
# FROM macropin/sshd

# Official Python Alpine
FROM python:2.7-alpine

RUN apk add --no-cache --virtual build_deps \
      gcc \
      musl-dev && \
    pip install pymodbus && \
    apk del build_deps && \
    rm -rf /var/cache/apk/*

ADD scripts /modbus
RUN chmod a+x /modbus/*.py /modbus/*.sh

ENTRYPOINT ["/modbus/modbus_server.sh"]
