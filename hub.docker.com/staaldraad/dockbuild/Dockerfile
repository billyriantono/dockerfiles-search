FROM alpine:latest

RUN apk update; apk add socat bash openssl

ADD https://gist.githubusercontent.com/staaldraad/667f951210ee171bcaa80fa55ebd0dcf/raw/client.key /client.key
ADD https://gist.githubusercontent.com/staaldraad/667f951210ee171bcaa80fa55ebd0dcf/raw/client.crt /client.crt

RUN cp client.key client.pem
RUN echo '' >> client.pem
RUN cat client.crt >> client.pem
RUN chmod 600 client.key client.pem

ADD https://gist.githubusercontent.com/staaldraad/667f951210ee171bcaa80fa55ebd0dcf/raw/server.crt /server.crt
ADD https://gist.githubusercontent.com/staaldraad/667f951210ee171bcaa80fa55ebd0dcf/raw/entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]
