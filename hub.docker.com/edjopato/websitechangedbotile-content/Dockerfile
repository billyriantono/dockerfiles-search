FROM golang:1.12-alpine
LABEL Author=edgar@edgarneto.com
RUN apk add --no-cache ca-certificates git
RUN mkdir /app 
ADD . /app/
WORKDIR /app
RUN go get "github.com/gorilla/mux"
RUN go build -o main .
RUN adduser -S -D -H -h /app appuser
USER appuser
EXPOSE 4000
ENTRYPOINT [ "./main" ]

