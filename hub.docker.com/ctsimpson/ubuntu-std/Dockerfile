FROM ubuntu:xenial
MAINTAINER chrsimpson
RUN apt-get update && apt-get install -y \
gcc \
build-essential \
make \
python-mysql.connector \
vim \
net-tools \
ssh \
wget \
sudo \
less \
inetutils-ping \
curl
COPY docker-entrypoint.sh /docker-entrypoint.sh
EXPOSE 22/tcp
LABEL relase-notes="Basic Ubuntu Build"
ENTRYPOINT ["/docker-entrypoint.sh"]
