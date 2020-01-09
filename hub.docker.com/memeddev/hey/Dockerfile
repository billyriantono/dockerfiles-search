FROM alpine:3.10.3
MAINTAINER memed <gabriel.couto@memed.com.br>

RUN wget -O /bin/hey https://storage.googleapis.com/hey-release/hey_linux_amd64 && chmod +x /bin/hey

CMD ["/bin/hey"]
