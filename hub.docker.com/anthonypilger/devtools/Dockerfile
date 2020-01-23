FROM docker:latest

RUN apk add --no-cache openssh-client python3; \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools awscli && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

COPY entrypoint /usr/local/bin/activate_swarm
ENTRYPOINT ["/usr/local/bin/activate_swarm"]
CMD ["sh"]
