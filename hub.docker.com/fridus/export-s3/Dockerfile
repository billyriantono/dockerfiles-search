FROM alpine:3.9

RUN apk add curl python3 && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py --user && \
    export PATH=~/.local/bin:$PATH && \
    pip3 install awscli --upgrade --user

COPY export-s3 /usr/local/bin
ENV PATH="/root/.local/bin:${PATH}"

ENTRYPOINT [ "export-s3" ]
