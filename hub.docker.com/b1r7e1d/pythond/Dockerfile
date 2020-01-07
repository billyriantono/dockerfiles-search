FROM ubuntu

RUN apt update && apt upgrade -y && \
    apt install git -y && \
    apt install python3.7 -y && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

ENTRYPOINT [ "/usr/bin/python3.7"]