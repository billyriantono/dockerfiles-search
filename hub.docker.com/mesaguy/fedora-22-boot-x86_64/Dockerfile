# Source
FROM fedora:22

# Strip down systemd
RUN for f in /lib/systemd/system/sysinit.target.wants/* ; do if [ "$(basename "$f")" != "systemd-tmpfiles-setup.service" ] ; then rm -f "$f" ; fi ; done && \
rm -f /lib/systemd/system/multi-user.target.wants/* && \
rm -f /etc/systemd/system/*.wants/* && \
rm -f /lib/systemd/system/local-fs.target.wants/* && \
rm -f /lib/systemd/system/sockets.target.wants/*udev* && \
rm -f /lib/systemd/system/sockets.target.wants/*initctl* && \
rm -f /lib/systemd/system/basic.target.wants/* && \
rm -f /lib/systemd/system/anaconda.target.wants/*

# Without this, init won't start the enabled services. Starting the services
# fails with one of:
#     Failed to get D-Bus connection: Operation not permitted
#     System has not been booted with systemd as init system (PID 1). Can't operate.
#     Failed to connect to bus: No such file or directory
VOLUME [ "/sys/fs/cgroup", "/run" ]

# Start via systemd
CMD ["/usr/lib/systemd/systemd"]

# Image metadata
LABEL org.label-schema.vendor="Mesaguy" \
      org.label-schema.name="Fedora Linux 22 boot" \
      org.label-schema.description="Image boots Fedora Linux 22 via systemd" \
      com.mesaguy.operatingsystem.eol="true"
