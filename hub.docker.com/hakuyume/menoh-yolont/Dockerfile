FROM alpine AS builder

ARG VERSION=2.1.2

RUN apk add --update curl 
RUN mkdir /tools
RUN curl -O -L https://github.com/rabbitmq/rabbitmq-perf-test/releases/download/v${VERSION}/rabbitmq-perf-test-${VERSION}-bin.tar.gz
RUN tar xvfz rabbitmq-perf-test-${VERSION}-bin.tar.gz -C /tools
RUN mv /tools/rabbitmq-perf-test-${VERSION} /tools/rabbitmq-perf-test

FROM anapsix/alpine-java:8
ENV PATH /tools/rabbitmq-perf-test/bin:$PATH
COPY --from=builder /tools/ /tools/
ENTRYPOINT [ "runjava", "com.rabbitmq.perf.PerfTest" ]