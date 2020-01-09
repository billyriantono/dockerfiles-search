FROM ubuntu:16.04

LABEL maintainer="onwsk8r@gmail.com" \
      description="Install an NBSP Server"
EXPOSE 8015 8016
HEALTHCHECK --start-period=5s --timeout=2s CMD curl localhost:8015 &> /dev/null

# Use this to specify a particular nbsp version
ENV NBSP_VERSION="nbsp-2.3.9p3"

# Note - curl is used by HEALTHCHECK and we use ntpdate
# because times are important
ADD ./install_latest_version.sh /sbin
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install curl ntpdate && \
    /sbin/install_latest_version.sh && \
    apt-get clean

ADD ./run.sh /
ENTRYPOINT ["/bin/bash", "-l", "/run.sh"]
