FROM alpine:latest

RUN apk add --no-cache python3 && \
    pip3 install --upgrade pip setuptools httpie~=0.9 && \
    rm -r /root/.cache

ENTRYPOINT [ "http" ]
CMD ["--help"]