FROM jaromirpufler/docker-openssh-client

RUN apk add --no-cache rsync tzdata

ADD entrypoint.sh /bin

WORKDIR /root/.ssh
VOLUME /root/.ssh

WORKDIR /data
ENTRYPOINT ["/bin/entrypoint.sh"]
CMD ["crond", "-f", "-L", "/dev/stdout"]
