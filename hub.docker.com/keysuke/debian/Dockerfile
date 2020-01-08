FROM docker.io/debian:latest

ENV DEBIAN_FRONTEND noninteractive

RUN rm -rf /etc/apt/sources.list.d/*

COPY debian9_sources_us /etc/apt/sources.list

RUN ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN apt-get update -q=2 && apt-get dist-upgrade -yq=2 -t stretch-backports && \
	apt-get install -yq=2 -t stretch-backports \
	neovim zsh git tig tree wget rsync curl openssl xclip xauth ncdu lsof mlocate \
	ack ccze pdsh \
	atop htop apachetop dstat iotop glances \
	tmux screen multitail byobu \
	logrotate logwatch strace \
	lynis nikto \
	ngrep nload nethogs iftop hping3 autossh net-tools mtr iproute tcpdump telnet traceroute dnsutils whois dhcping \
	elinks jq \
	unzip unrar p7zip \
	sl cowsay \
	openssh-server \
	locales dialog aptitude dpkg-dev rsyslog \
	systemd-sysv && \
	apt-get clean

ENV LANG fr_FR.UTF-8
RUN rm -rf /var/lib/apt/lists/* && \
	sed -i -e "s/# fr_FR.UTF-8.*/fr_FR.UTF-8 UTF-8/" /etc/locale.gen && \
	localedef -c -i fr_FR -f UTF-8 fr_FR.UTF-8 && \
	update-locale LANG=fr_FR.UTF-8 && \
	dpkg-reconfigure --frontend=noninteractive locales && \
	chsh -s /usr/bin/zsh

RUN sed -i '/ssh_host_ed25519_key/s/^#//' /etc/ssh/sshd_config && \
	sed -i '/#AddressFamily any/s/^#//'  /etc/ssh/sshd_config && \
	sed -i '/AddressFamily any/s/any/inet/'  /etc/ssh/sshd_config && \
	sed -i '/#PasswordAuthentication yes/s/^#//'  /etc/ssh/sshd_config && \
	sed -i '/PasswordAuthentication/s/yes/no/' /etc/ssh/sshd_config && \
	sed -i '/#PermitRootLogin yes/s/yes/prohibit-password/' /etc/ssh/sshd_config && \
	sed -i '/#PermitRootLogin/s/^#//' /etc/ssh/sshd_config && \
	sed -i '/NAutoVTs/s/#NAutoVTs=6/NAutoVTs=0/' /etc/systemd/logind.conf && \
	sed -i '/ReserveVT/s/#ReserveVT=6/ReserveVT=0/' /etc/systemd/logind.conf && \
	echo "Ciphers chacha20-poly1305@openssh.com" >> /etc/ssh/sshd_config && \
	echo "KexAlgorithms curve25519-sha256@libssh.org" >> /etc/ssh/sshd_config && \
	echo "MACs hmac-sha2-512-etm@openssh.com" >> /etc/ssh/sshd_config && \
	echo "DebianBanner no" >> /etc/ssh/sshd_config && \
	echo "_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=lcd -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel -Dswing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'" >> /etc/environment && \
	rm /etc/motd && \
	systemctl disable getty@tty1.service && \
	sed -i '/ftp.us.debian/s/us/fr/g' /etc/apt/sources.list

COPY home /root

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]
