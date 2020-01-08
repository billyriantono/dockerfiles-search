FROM evarga/jenkins-slave

RUN apt-get update && \
    apt-get -q install -y  \
        ca-certificates \
        curl \
        openssl

RUN apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin

ENV DOCKER_BUCKET get.docker.com
ENV DOCKER_VERSION 1.11.2
ENV DOCKER_SHA256 8c2e0c35e3cda11706f54b2d46c2521a6e9026a7b13c7d4b8ae1f3a706fc55e1

RUN set -x \
    && curl -fSL "https://${DOCKER_BUCKET}/builds/Linux/x86_64/docker-$DOCKER_VERSION.tgz" -o docker.tgz \
    && echo "${DOCKER_SHA256} *docker.tgz" | sha256sum -c - \
    && tar -xzvf docker.tgz \
    && mv docker/* /usr/local/bin/ \
    && rmdir docker \
    && rm docker.tgz \
    && docker -v

RUN groupadd docker && \
    chgrp docker /usr/local/bin/docker && \
    chmod +s /usr/local/bin/docker && \
    usermod -aG docker jenkins

COPY docker-entrypoint.sh ./
RUN chmod 755 ./docker-entrypoint.sh
ENTRYPOINT ["./docker-entrypoint.sh"]

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]
