FROM openjdk:8u171-alpine3.7

COPY agent.jar /

COPY agent.sh /

COPY requirements.txt /tmp/

RUN chmod +x /agent.jar /agent.sh && \
    apk add --no-cache --update \
    bash \
    ca-certificates \
    curl \
    git \
    openssh-client \
    nano \
    python \
    py-pip \
    \
    && pip install --requirement /tmp/requirements.txt \
    \
    # Cleanup
    && rm -rf /tmp/* /var/tmp/*


CMD ["/agent.sh"]
