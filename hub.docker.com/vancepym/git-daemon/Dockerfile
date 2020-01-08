FROM ubuntu:xenial-20170119
MAINTAINER Scott Fan <fancp2007@gmail.com>

RUN apt update && \
    apt install -y --no-install-recommends git-daemon-run && \
    rm -rf /var/lib/apt/lists/*

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen --purge en_US.UTF-8 && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN sed -e 's|chpst -ugitdaemon|chpst -uroot|' -e 's|--verbose --reuseaddr|--verbose --export-all --reuseaddr|' -i /etc/sv/git-daemon/run && \
    sed -e 's|--base-path=/var/lib /var/lib/git|--base-path=/var/cache/git|' -i /etc/sv/git-daemon/run && \
    sed '3a rm -rf /var/cache/git && mkdir -p /var/cache/git && ln -sf /git/repositories/* /var/cache/git/' -i /etc/sv/git-daemon/run

VOLUME /git/repositories

EXPOSE 9418

CMD ["/etc/sv/git-daemon/run"]
