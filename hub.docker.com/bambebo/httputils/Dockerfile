FROM alpine:3.7

RUN apk add --no-cache curl bind-tools python3 jq bash && \
    pip3 install --upgrade pip setuptools httpie && \
    rm -r /root/.cache

ENTRYPOINT ["sleep","1000000"]