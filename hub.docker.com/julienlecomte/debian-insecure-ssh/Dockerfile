FROM  debian:stretch-slim
LABEL maintainer="Julien Lecomte <julien@lecomte.at>"

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    openssh-server \
 && rm -fr /var/lib/apt/lists/* \
 && rm -fr /usr/share/man/* /usr/share/doc/* /usr/share/info/* \
 && mkdir /run/sshd \
 && true

ADD from/debian/stretch-slim/fs /

EXPOSE 22 

ENTRYPOINT ["/usr/sbin/sshd"]
CMD ["-D", "-e"]

