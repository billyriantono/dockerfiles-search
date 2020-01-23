FROM golang:latest 
RUN mkdir /app 
ADD . /app/ 
WORKDIR /app 
RUN go get github.com/go-kit/kit/endpoint
RUN go get github.com/go-logfmt/logfmt
RUN go get github.com/prometheus/client_golang/prometheus
RUN go build -o main . 
CMD ["/app/main"]