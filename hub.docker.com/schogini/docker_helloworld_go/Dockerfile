FROM golang:1.8
COPY hello.go /
WORKDIR /
RUN go build hello.go
CMD ["./hello"]


# docker build -t gohw . 
# docker run -ti -e a=20 -e b=21 gohw
