FROM golang:alpine AS gobuilder

RUN apk --no-cache add build-base git

COPY . /project
WORKDIR /project
RUN go build -o redirector

FROM alpine:latest

COPY --from=gobuilder /project/redirector /redirector
CMD /redirector
