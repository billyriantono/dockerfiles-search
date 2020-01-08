FROM debian:latest

COPY . /app

RUN apt-get update && apt-get install -y g++ make libssl-dev libboost-all-dev && cd /app && make

ENTRYPOINT [ "/app/dnsseed" ]

EXPOSE 53/udp
