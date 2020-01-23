FROM alpine:3.10

COPY includes/requirements.txt /

RUN apk add --no-cache \
        python3 \
    && pip3 install --upgrade pip \
    && pip3 install -r /requirements.txt

COPY includes/*.py /usr/bin/

ENTRYPOINT ["/usr/bin/imap_count.py", "/etc/imap_count.yaml"]
