FROM debian:latest
RUN apt-get update && \
    apt-get install -y ca-certificates && \
    apt-get install -y wget && \
    apt-get install -y libxml-xpath-perl && \
    apt-get install -y curl && \
    apt-get install -y git && \
    apt-get install -y dos2unix
ENV DOCKER_CHANNEL stable
ENV DOCKER_VERSION 18.06.2-ce
RUN set -eux && debianArch="x86_64" && wget -O docker.tgz "https://download.docker.com/linux/static/${DOCKER_CHANNEL}/${debianArch}/docker-${DOCKER_VERSION}.tgz" && tar --extract --file docker.tgz --strip-components 1 --directory /usr/local/bin/ && rm docker.tgz && dockerd --version && docker --version	
COPY modprobe.sh /usr/local/bin/modprobe
COPY docker-entrypoint.sh /usr/local/bin/
