FROM golang:latest
MAINTAINER Marshall Lee <marshall.s.lee@gmail.com>

RUN mkdir /app

ADD app /app/app
ADD cmd/chitchat-tokens /app/cmd/chitchat-tokens
ADD config /app/config
ADD consts /app/consts
ADD handler /app/handler
ADD models /app/models
ADD response /app/response

WORKDIR /app/cmd/chitchat-tokens
COPY . .

RUN go get -t github.com/gorilla/mux
RUN go get -t github.com/newrelic/go-agent
RUN go get -t gopkg.in/yaml.v2
RUN go get -t github.com/go-redis/redis
RUN go get -t github.com/tidwall/gjson
RUN go get -t github.com/valyala/fasthttp
RUN go get -t github.com/valyala/fasthttp/fasthttpadaptor

EXPOSE 12385

RUN go build -o chitchat-tokens .

CMD ./chitchat-tokens