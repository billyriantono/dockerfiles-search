FROM debian:stretch-slim

EXPOSE 139
EXPOSE 445

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y samba samba-vfs-modules libnss-winbind

ENTRYPOINT ["/usr/sbin/smbd"]
CMD ["-F", "-S"]
