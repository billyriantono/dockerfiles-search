FROM golang:latest
ADD . /go/src/mailservice
RUN cd /go/src/mailservice && go get && go install
ENTRYPOINT /go/bin/mailservice
ENV MG_DOMAIN sandboxf0c9c903d8e94aebb6dc6b909843f89f.mailgun.org
ENV MG_API_KEY key-9b646b9e39521cf970ca4c2d1118d227
ENV MG_PUBLIC_API_KEY pubkey-96a1a9f7ddef228fe3e6b5088577b5be
ENV MAIL_SERVICE_PORT 9001
ENV UMES_DOMAIN http://localhost:9801
EXPOSE 9001