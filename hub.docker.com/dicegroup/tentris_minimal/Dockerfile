FROM ubuntu:19.04

RUN apt update && apt install  -y uuid-dev libserd-dev

COPY tentris_server /tentris_server

RUN  chmod +x /tentris_server

RUN mkdir -p logs

WORKDIR /logs

ENTRYPOINT ["/tentris_server"]
