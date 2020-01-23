FROM ubuntu:14.04
ENV DEBIAN_FRONTEND=noninteractive
RUN echo 'force-unsafe-io' > /etc/dpkg/dpkg.cfg.d/02apt-speedup \
    && apt-get update \
    && apt-get install --yes --no-install-recommends beanstalkd \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

VOLUME /data

EXPOSE 11300

ENTRYPOINT ["beanstalkd", "-p", "11300"]
CMD ["-b", "/data"]
