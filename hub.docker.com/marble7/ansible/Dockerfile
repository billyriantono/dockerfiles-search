FROM alpine:3.10

ENV ANSIBLE_VERSION=2.8.6 \
    ANSIBLE_HOST_KEY_CHECKING=False

RUN apk --no-cache add python3 openssl ca-certificates && \
    apk --no-cache add --virtual build-dependencies \
        python3-dev libffi-dev openssl-dev build-base && \
    pip3 install "ansible == ${ANSIBLE_VERSION}" && \
    apk del build-dependencies

ENTRYPOINT [ "ansible-playbook" ]
CMD ["--version" ]
