FROM alpine

RUN apk update
RUN apk add bash curl coreutils git util-linux
RUN mkdir /app

WORKDIR /app

RUN git clone https://github.com/sahsanu/lectl.git /app

ENTRYPOINT ["bash", "/app/lectl"]
CMD []
