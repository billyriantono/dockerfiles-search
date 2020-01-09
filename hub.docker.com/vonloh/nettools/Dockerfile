FROM debian:stable-slim
RUN apt update \
    && apt install -y traceroute curl dnsutils netcat-openbsd jq nmap \ 
                          net-tools iputils-ping \
    && apt clean
COPY Dockerfile /Dockerfile
LABEL org.label-schema.docker.dockerfile="/Dockerfile" \
      org.label-schema.vcs-type="Git" \
      org.label-schema.vcs-url="https://github.com/vonloh/network-utils"    