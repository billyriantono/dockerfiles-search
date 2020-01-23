FROM golang as builder

WORKDIR /work

COPY a.go /work/

RUN go build a.go

FROM scratch

COPY --from=builder /work/a /a

CMD ["/a"]

WORKDIR /home/nacos/plugins/mysql

ADD https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.18/mysql-connector-java-8.0.18.jar .
