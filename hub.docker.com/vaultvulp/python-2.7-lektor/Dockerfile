FROM node:11 as node
LABEL maintainer="VaultVulp"
WORKDIR /lektor

RUN git clone https://github.com/lektor/lektor . && \
    make build-js

FROM python:2.7
WORKDIR /blog

COPY --from=node /lektor /lektor

RUN pip install -U pip && \
    pip install /lektor

EXPOSE 5000

CMD ["lektor", "serve", "-h", "0.0.0.0" ]
