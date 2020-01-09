FROM ubuntu
Maintainer Pavo <brockbackups@gmail.com>
RUN apt-get update && apt-get install -y wget subversion uuid-dev python build-essential
VOLUME /root/src
COPY setup.sh /root
RUN chmod +x /root/setup.sh
ENTRYPOINT /root/setup.sh
