FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt update && apt install -y \
  linux-generic \
  xfsprogs \
  grub-pc \
  cryptsetup \
  mdadm \
  lvm2 \
  openssh-server \
  dropbear \
  busybox \
  ifupdown \
  net-tools \
  iputils-ping \
  rsyslog \
  iptables \
  ntp \
  ferm \
  strace \
  lsof \
  tcpdump \
  ngrep \ 
  telnet \
  netcat-openbsd \
  vim \
  && apt remove -y unattended-upgrades \
  && \
  update-rc.d -f dropbear remove              #Disable dropbear SSH server after OS boot

RUN mkdir -p /root/.ssh/                                                   && \
  chmod 0755 /root/.ssh/                                                   && \
  rm -v /etc/ssh/ssh_host_* /etc/dropbear*/dropbear_*_host_key             && \
  echo CRYPTSETUP=y                >/etc/initramfs-tools/conf.d/cryptsetup && \
  echo -e "LANG=C\nLC_ALL=C"                          >>  /etc/environment && \
  echo '/dev/mapper/vg-root / xfs defaults 0 1'>   /etc/fstab       && \
  sed  -i 's/_LINUX=.*$/_LINUX="net.ifnames=0 debug=vc"/' /etc/default/grub
