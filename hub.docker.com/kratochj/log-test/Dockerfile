FROM alpine:3.8

LABEL org.label-schema.schema-version = "1.0"
LABEL org.label-schema.description = "Simple image that periodicaly prints random log messages"
LABEL org.label-schema.url="https://github.com/kratochj/docker-advance-training-excercise-solutions/tree/master/logging_test"
LABEL org.label-schema.vendor = "Jiri Kratochvil"
LABEL org.label-schema.docker.cmd="docker run -it kratochj/log-test"

RUN apk --no-cache add bash

WORKDIR /tmp
ADD . .

CMD /tmp/run.sh
