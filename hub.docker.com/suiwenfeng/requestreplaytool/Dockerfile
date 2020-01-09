FROM alpine
ENV RATE "|500%"
ENV URL "127.0.0.1:8080"
COPY *.gor /
COPY supervisord.conf /
RUN apk add bash supervisor go git libpcap-dev musl-dev
RUN go get -v github.com/buger/goreplay
ENTRYPOINT ["/usr/bin/supervisord", "-n" , "-c", "supervisord.conf"]
