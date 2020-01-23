FROM openjdk:8-slim

RUN apt-get update && apt-get install --no-install-recommends -y \
        curl \
        wget \
        tar \
        git \
        fish \
        man \
        sudo \
    && rm -rf /var/lib/apt/lists/* \
    && useradd -ms /usr/bin/fish developer \
    && echo "developer ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR /opt/idea

RUN curl -fsSL https://download.jetbrains.com/idea/ideaIU-2018.3.2.tar.gz -o /opt/idea/idea.tar.gz \
    && tar xvzf idea.tar.gz --strip-components=1 \
    && chown -R developer:developer  /opt/idea \
    && rm idea.tar.gz

ENV DOCKER_VERSION 18.09.0
RUN wget -O docker.tgz "https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz" \
    && tar --extract \
       		--file docker.tgz \
       		--strip-components 1 \
       		--directory /usr/local/bin/ \
    && rm docker.tgz

USER developer

SHELL ["/usr/bin/fish", "-c"]
COPY ultimate-docker/entrypoint /
ENTRYPOINT ["sudo", "/entrypoint"]
CMD ["/opt/idea/bin/idea.sh" ]
