FROM mongo:latest

MAINTAINER xjd <25635680@qq.com>

RUN apt-get update && apt-get install -y ssh-client expect --no-install-recommends \
&& rm -rf /var/lib/apt/lists/*

COPY ./backup-entrypoint.sh  /
ENTRYPOINT ["/backup-entrypoint.sh"]
