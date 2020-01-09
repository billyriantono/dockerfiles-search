FROM python:alpine

RUN apk add --no-cache gcc musl-dev libffi-dev openssl-dev && \
    pip install moto[server] && \
    apk del gcc musl-dev libffi-dev openssl-dev

ENTRYPOINT ["moto_server"]
