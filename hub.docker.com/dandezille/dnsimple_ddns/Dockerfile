FROM alpine:3.10
RUN apk add --no-cache curl jq

# Copy app scripts
COPY *.sh /src/
RUN chmod +x /src/*.sh
WORKDIR /src/

# Default startup script
CMD sh /src/dnsimple-dynamic-dns.sh
