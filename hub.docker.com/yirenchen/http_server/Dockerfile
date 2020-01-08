FROM debian:jessie
MAINTAINER YRC <nthuyirenchen@gmail.com>
ADD ./server.c /home/
RUN apt-get update && \
apt-get install -y gcc && \
gcc /home/server.c -o /home/server.o && \
apt-get remove -y --auto-remove gcc && \
apt-get clean
ENTRYPOINT ["./home/server.o"]
