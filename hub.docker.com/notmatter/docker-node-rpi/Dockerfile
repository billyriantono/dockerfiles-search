FROM resin/armv7hf-debian-qemu

RUN [ "cross-build-start" ]

RUN apt update && apt install curl && apt install git
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN apt update && apt install -y nodejs

CMD [ "node" ]
