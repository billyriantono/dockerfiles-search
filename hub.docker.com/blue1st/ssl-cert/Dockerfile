FROM alpine:latest

RUN apk add --update --no-cache openssl && \
		mkdir /ssl

WORKDIR /ssl

COPY ./create_cert /usr/local/bin/

CMD ["create_cert"]
