FROM alpine:3.5

# Run updates and install packages
RUN apk add --update python3 \
	&& pip3 install requests

# Copy application
COPY haproxy-to-graphite /haproxy-to-graphite

ENTRYPOINT [ "/usr/bin/python3", "-u", "/haproxy-to-graphite/app.py" ]