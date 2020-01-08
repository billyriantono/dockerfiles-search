FROM ubuntu:16.04
LABEL maintainer="jchm@infoinnova.net"

COPY install.sh /install.sh
RUN chmod +x /install.sh
RUN /install.sh

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENV MOUNTPOINT="/mnt/mountpoint" \
    CHUNKSIZE=10M \
    MAX_CHUNKS=1000 \
    CHUNKLOADAHEAD=15 \
    VERBOSITY=2 \
    REFRESH=60m

ENTRYPOINT ["/entrypoint.sh"]
CMD ["mount"]
