FROM ubuntu:trusty
MAINTAINER Wei-Tsung Lin <fasthall@gmail.com>

ENV TERM xterm

RUN apt-get update
RUN apt-get install -y nethogs iperf trickle

EXPOSE 5001

ENTRYPOINT ["/usr/bin/iperf"]
CMD ["-s"]
