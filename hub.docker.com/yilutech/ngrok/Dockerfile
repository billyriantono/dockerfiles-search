FROM golang:alpine

RUN apk update
RUN apk add --update alpine-sdk git

RUN git clone https://github.com/inconshreveable/ngrok.git /ngrok
COPY startup /startup
RUN chmod +x /startup

VOLUME [ "/ngrok/bin/windows_amd64" ]
EXPOSE 4443 80 443
WORKDIR /ngrok
CMD ["/startup"]