FROM amd64/ubuntu:18.04
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends nfs-kernel-server man-db nano tzdata && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN mkdir -p /exports
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +rx /usr/local/bin/docker-entrypoint.sh
VOLUME /exports
EXPOSE 2049/tcp
EXPOSE 20048/tcp
ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
CMD ["/exports"]
