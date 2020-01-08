FROM debian:latest

ENV DEBIAN_FRONTEND noninteractive
ENV container docker

MAINTAINER keoni84 <keoni84@gmail.com>

# add contrib, non-free and backports repositories & set preferences
ADD sources.list /etc/apt/sources.list
ADD preferences /etc/apt/preferences

# Install some base utilities & clean
RUN apt-get -y update && apt-get -y upgrade && apt-get clean && \
		apt-get -y install apt-utils lsb-release curl git cron at logrotate rsyslog \
			unattended-upgrades ssmtp lsof locales procps \
			initscripts libsystemd0 libudev1 systemd sysvinit-utils udev util-linux && \
		dpkg-reconfigure locales && \
		apt-get clean

# Set root password
RUN echo root && echo "root:root" | chpasswd

# Add unattended upgrades & config
ADD apt_unattended-upgrades /etc/apt/apt.conf.d/50unattended-upgrades
ADD apt_periodic /etc/apt/apt.conf.d/02periodic

RUN cd /lib/systemd/system/sysinit.target.wants/ && \
		ls | grep -v systemd-tmpfiles-setup.service | xargs rm -f && \
		rm -f /lib/systemd/system/sockets.target.wants/*udev* && \
		systemctl mask -- \
			tmp.mount \
			etc-hostname.mount \
			etc-hosts.mount \
			etc-resolv.conf.mount \
			-.mount \
			swap.target \
			getty.target \
			getty-static.service \
			dev-mqueue.mount \
			systemd-tmpfiles-setup-dev.service \
			systemd-remount-fs.service \
			systemd-ask-password-wall.path \
			systemd-logind.service && \
		systemctl set-default multi-user.target || true

RUN sed -ri /etc/systemd/journald.conf \
			-e 's!^#?Storage=.*!Storage=volatile!'
ADD container-boot.service /etc/systemd/system/container-boot.service
RUN mkdir -p /etc/container-boot.d && \
		sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
		echo "LANG=en_US.UTF-8" >> /etc/default/locale && \
		echo "export LC_ALL=en_US.UTF-8" >> /etc/bash.bashrc && \
		echo "export LANG=en_US.UTF-8" >> /etc/bash.bashrc && \
		echo "export LANGUAGE=en_US.UTF-8" >> /etc/bash.bashrc && \
		/usr/sbin/locale-gen && \
		echo "alias ll='ls -l'" >> /root/.bashrc && \
		systemctl enable container-boot.service && systemctl mask cgproxy

VOLUME [ "/sys/fs/cgroup", "/run", "/run/lock", "/tmp" ]
CMD ["/lib/systemd/systemd"]