FROM alpine:3.7

RUN apk --update-cache add curl
RUN curl -o /usr/local/bin/cfssl https://pkg.cfssl.org/R1.2/cfssl_linux-amd64
RUN curl -o /usr/local/bin/cfssljson https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
RUN chmod +x /usr/local/bin/cfssl*

RUN mkdir /assets
ADD assets/* /assets/

VOLUME /certs

COPY script/generate.sh /

CMD ["/bin/sh","/generate.sh"]

