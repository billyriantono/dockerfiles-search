FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y socat

CMD ["socat", "TCP-LISTEN:2375,reuseaddr,fork", "UNIX-CLIENT:/var/run/docker.sock"]
