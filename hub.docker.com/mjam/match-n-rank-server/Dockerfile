FROM golang:1.13-alpine AS builder

RUN apk update
RUN apk add --no-cache git openssh gcc libc-dev

RUN mkdir -p /matchnrank
WORKDIR /matchnrank

COPY server/go.mod server/go.sum ./
RUN go mod download

COPY server/ .
WORKDIR /matchnrank/cmd/matchnrank
RUN GOOS=linux GOARCH=amd64 go build -a -tags netgo -ldflags '-w -extldflags "-static"' -o /matchnrank/bin/matchnrank

FROM alpine
COPY --from=builder /matchnrank/bin/matchnrank /matchnrank/bin/matchnrank
COPY --from=builder /matchnrank/docs /matchnrank/docs
WORKDIR /matchnrank
CMD /matchnrank/bin/matchnrank
