FROM golang:1.9-alpine

RUN apk add --no-cache git docker bash
RUN go get github.com/yudai/gotty

ADD run.sh run.sh
RUN chmod 700 run.sh
ENTRYPOINT gotty --title-format "Panux Demo" --close-signal "1" --max-connection "20" -w bash run.sh
