FROM debian:stretch-slim

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y winbind libnss-winbind

ENTRYPOINT ["/usr/sbin/winbindd"]
CMD ["-F", "-S"]
