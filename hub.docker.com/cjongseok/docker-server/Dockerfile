#
# It assumes docker.sock is at /var/run/docker.sock
#
# Author: Jongseok Choi
#
FROM ubuntu:14.04

RUN apt-get update && \
 apt-get install -y socat

CMD ["socat", "tcp-listen:4243,fork,reuseaddr", "unix-client:/var/run/docker.sock"]
