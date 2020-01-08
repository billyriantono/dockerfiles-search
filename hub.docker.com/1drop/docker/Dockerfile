FROM docker:git

RUN apk update -q && apk add -q --no-progress py-pip bash curl && rm -rf /var/cache/apk/*
RUN pip install -q docker-compose
ADD https://github.com/git-lfs/git-lfs/releases/download/v2.2.0/git-lfs-linux-amd64-2.2.0.tar.gz /tmp/
RUN cd /tmp/ && tar xzf git-lfs-linux-amd64-2.2.0.tar.gz && cd git-lfs-2.2.0 && ./install.sh && cd .. && rm -rf git-*
RUN curl -L https://github.com/docker/machine/releases/download/v0.12.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine \
	&& chmod +x /tmp/docker-machine \
	&& cp /tmp/docker-machine /usr/local/bin/docker-machine
