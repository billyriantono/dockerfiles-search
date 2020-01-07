FROM alpine

RUN apk add --no-cache bash curl git openssh-client

ENV VERSION "18.03.0-ce"

ENV DOCKER_AWS_TOOL_DIR=/usr/local/docker-aws-tool/

ENV PATH=$PATH:$DOCKER_AWS_TOOL_DIR

# Install docker 
RUN curl -L -o /tmp/docker-$VERSION.tgz https://download.docker.com/linux/static/stable/x86_64/docker-$VERSION.tgz \
    && tar -xz -C /tmp -f /tmp/docker-$VERSION.tgz \
    && mv /tmp/docker/docker /usr/bin \
    && rm -rf /tmp/docker-$VERSION /tmp/docker
    
# Install AWS CLI
RUN \
	mkdir -p /aws && \
	apk -Uuv add groff less python py-pip && \
	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/*

# Install scripts    
COPY scripts/* $DOCKER_AWS_TOOL_DIR

WORKDIR /home

CMD ["help"]