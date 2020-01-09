FROM crystallang/crystal:0.26.0-build

ADD . /app
WORKDIR /app
RUN crystal build --release src/ping-request.cr

FROM ubuntu:xenial

RUN apt-get update && apt-get -y install libssl1.0 libevent-2.0 inetutils-ping && apt-get clean && rm -rf /var/lib/apt/lists/*

COPY --from=0 /app/ping-request /ping-request

EXPOSE 8080
CMD /ping-request
