FROM ubuntu
MAINTAINER Shay Erlichmen "shay@samba.me"

run echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
run apt-get update
run apt-get -y upgrade
run apt-get install -y -qq wget git
run wget -qO- http://go.googlecode.com/files/go1.2.linux-amd64.tar.gz | tar xz -C /usr/local
env HOME /root
env GOPATH /root/go
env PATH /usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

run go get github.com/bitly/google_auth_proxy
expose 8080 4180
entrypoint ["/root/go/bin/google_auth_proxy"]