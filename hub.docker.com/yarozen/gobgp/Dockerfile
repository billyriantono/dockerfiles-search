FROM alpine:latest

MAINTAINER Yaniv Rozenboim <yanivr@radware.com>

RUN mkdir gobgp \
    && cd gobgp \
    && wget https://github.com/osrg/gobgp/releases/download/v1.33/gobgp_1.33_linux_386.tar.gz \
    && tar xvfz gobgp_1.33_linux_386.tar.gz \
    && rm gobgp_1.33_linux_386.tar.gz

ENTRYPOINT ["/gobgp/gobgpd"]

EXPOSE 50051
