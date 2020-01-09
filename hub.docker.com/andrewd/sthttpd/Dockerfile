FROM alpine:3.2
MAINTAINER Andrew Dunham <andrew@du.nham.ca>

# Add binary and init script
ADD thttpd init /

# Copy into place.
RUN mkdir -p /usr/local/bin && \
    echo "Copying thttpd" && \
    chown root:root /thttpd && \
    chmod +x /thttpd && \
    mv /thttpd /usr/local/bin/ && \
    echo "Copying init" && \
    chown root:root /init && \
    chmod +x /init && \
    mv /init /usr/local/bin/

# Put data files to be served here.
VOLUME ["/data"]

CMD ["/usr/local/bin/init"]
