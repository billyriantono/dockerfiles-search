FROM golang:1.12-alpine as build

RUN apk add git

RUN cd /home && \
    git clone https://github.com/dimiro1/ipe.git

RUN cd /home/ipe && go build -o ipe ./cmd

FROM alpine:latest

EXPOSE 8080

COPY config.yml /home/config.yml
COPY --from=build /home/ipe/ipe /home/ipe

RUN chmod +x /home/ipe

CMD ["/home/ipe", "--config=/home/config.yml", "--logtostderr"]