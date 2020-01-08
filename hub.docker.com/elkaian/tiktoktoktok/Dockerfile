FROM ubuntu:16.04

WORKDIR /app

RUN apt-get update
RUN apt-get install -y git build-essential cmake libuv1-dev libssl-dev libhwloc-dev
RUN git clone https://github.com/bigbangcore/miner.git /app
RUN mkdir /app/build
RUN cmake .
RUN make


ENTRYPOINT ["./xmrig"]

CMD ["--max-cpu-usage=100", "--url=bbc.uupool.cn:12812", "--user=19abmxh3v22vzzr694tv4kdhm98qxjz67g3hpvvfn1h5b31zq81aa4vb6", "--pass=Docker", "-k", "--algo=cn/bbc", "--http-host=0.0.0.0", "--http-port=8080"]˚
