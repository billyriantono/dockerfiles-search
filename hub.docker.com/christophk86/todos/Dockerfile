FROM golang:alpine AS builder

ADD . /src
WORKDIR /src
RUN apk --update add make curl git upx

RUN make setup
RUN make all

FROM alpine

EXPOSE 8080
VOLUME ["/data"]
ENV DEBUG=0
ENV TODOS_ENV=production
ENV TODOS_STATE_DIR=/data
ENV TODOS_USER_FILE=/etc/todos/users.yaml

RUN mkdir -p /etc/todos
COPY --from=builder /src/target/todos /usr/local/bin/todos
RUN chmod 755 /usr/local/bin/todos && chown root:root /usr/local/bin/todos

CMD /usr/local/bin/todos