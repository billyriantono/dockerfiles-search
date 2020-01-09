FROM alpine:3.7

EXPOSE 2222

# openssh
RUN \
  apk add --update --no-cache openssh \
  && echo "root:Docker!" | chpasswd \
  && ssh-keygen -A

COPY etc/sshd_config /etc/ssh/
RUN chmod 644 /etc/ssh/sshd_config

# openrc
RUN \
  apk add --update --no-cache openrc \
  && sed -i 's/#rc_sys=""/rc_sys="lxc"/g' /etc/rc.conf \
  && echo 'rc_provide="loopback net"' >> /etc/rc.conf \
  && sed -i 's/^#\(rc_logger="YES"\)$/\1/' /etc/rc.conf \
  && sed -i '/tty/d' /etc/inittab \
  && sed -i 's/hostname $opts/# hostname $opts/g' /etc/init.d/hostname \
  && sed -i 's/mount -t tmpfs/# mount -t tmpfs/g' /lib/rc/sh/init.sh \
  && sed -i 's/cgroup_add_service /# cgroup_add_service /g' /lib/rc/sh/openrc-run.sh

# tools
RUN \
  apk add --update --no-cache \
    curl \
    git
