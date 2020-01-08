FROM ubuntu:16.04
MAINTAINER ZeroneVu <zeronevu@gmail.com>

# gcc for cgo, and all other common packages
RUN apt-get update && apt-get install -y --no-install-recommends \
  curl \
  ca-certificates \
  build-essential \		
  git \
  mercurial \
  bzr \
  && rm -rf /var/lib/apt/lists/*

# Starting environment config, download the go source file
ENV GOLANG_VERSION 1.8.1
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 a579ab19d5237e263254f1eac5352efcf1d70b9dacadb6d6bb12b0911ede8994

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz

ENV GOPATH /home/work
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/

# Some utilities scripts from github
RUN mkdir -p /script
RUN git -C /script clone https://github.com/ZeroneVu/shell.git ./

# Installing cron ... need some jobs too. All of us too

RUN apt-get update && apt-get install -y --no-install-recommends \
  cron \
  && rm -rf /var/lib/apt/lists/*

COPY crontab.txt /var/crontab.txt
RUN crontab /var/crontab.txt
RUN chmod 600 /etc/crontab

# Supervisor and configuration
RUN apt-get update && apt-get install -y --no-install-recommends \
  supervisor \
  && rm -rf /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]