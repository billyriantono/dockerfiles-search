FROM alpine:latest

WORKDIR /workspace

RUN apk update \ 
 && apk add --no-cache git pkgconfig gcc linux-headers libc-dev libffi-dev libgit2-dev \
 && apk add --no-cache python3-dev

RUN pip3 install --upgrade pip \
 && pip3 install ipython


RUN apk add --no-cache gcc musl-dev \ 
 && apk add --no-cache rust cargo

CMD ["/bin/sh"]


