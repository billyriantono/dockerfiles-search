FROM debian:wheezy

ENV DEBIAN_FRONTEND="noninteractive"

ADD /entrypoint.sh /

RUN \
	mkdir /gopath && \
	chmod +x /entrypoint.sh && \
	apt-get update && \
	apt-get install -y curl git && \
    curl https://storage.googleapis.com/golang/go1.7.3.linux-amd64.tar.gz | tar xz -C /usr/local && \
    echo "export PATH=\$PATH:/usr/local/go/bin" >> /etc/profile.d/golang.sh && \
    echo "export GOPATH=/gopath" >> /etc/profile.d/golang.sh && \
    apt-get autoremove --purge -y curl && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /gopath

ENTRYPOINT /entrypoint.sh