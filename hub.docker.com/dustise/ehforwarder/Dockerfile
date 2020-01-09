FROM alpine
COPY prepare.sh /usr/local/bin/sh/prepare.sh
RUN /usr/local/bin/sh/prepare.sh && \
    rm /usr/local/bin/sh/prepare.sh

VOLUME ["/efd"]
CMD ["ehforwarderbot"]

