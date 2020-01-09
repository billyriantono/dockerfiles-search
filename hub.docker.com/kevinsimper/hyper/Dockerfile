FROM debian:latest

RUN apt-get update && apt-get install -y wget && \
    wget https://hyper-install.s3.amazonaws.com/hyper-linux-x86_64.tar.gz && \
    tar xzf hyper-linux-x86_64.tar.gz && chmod +x ./hyper && mv hyper /usr/bin/

ENTRYPOINT ["hyper"]

CMD ["--help"]
