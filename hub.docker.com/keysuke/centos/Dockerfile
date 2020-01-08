FROM docker.io/centos:latest

ENV container docker

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
	systemd-tmpfiles-setup.service ] || rm -f $i; done); \
	rm -f /lib/systemd/system/multi-user.target.wants/*;\
	rm -f /etc/systemd/system/*.wants/*;\
	rm -f /lib/systemd/system/local-fs.target.wants/*; \
	rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
	rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
	rm -f /lib/systemd/system/basic.target.wants/*;\
	rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN yum upgrade -y && \
	yum install -y --nogpgcheck epel-release && \
	yum install -y --nogpgcheck \
	neovim zsh git tig tree wget rsync curl openssl xclip xauth ncdu lsof mlocate \
	ack ccze pdsh \
	atop htop apachetop dstat iotop glances \
	tmux screen multitail byobu \
	logrotate logwatch strace \
	lynis nikto \
	ngrep nload nethogs iftop hping3 autossh net-tools mtr iproute tcpdump telnet traceroute bind-utils whois dhcping \
	elinks jq \
	unzip unrar p7zip \
	sl cowsay \
	openssh-server openssh-clients dhclient iptables-services rsyslog && \
	yum clean all

RUN localedef -c -i fr_FR -f UTF-8 fr_FR.UTF-8 && \
	chsh -s /bin/zsh

RUN sed -i '/ssh_host_rsa_key/s/^/#/' /etc/ssh/sshd_config && \
	sed -i '/ssh_host_ecdsa_key/s/^/#/' /etc/ssh/sshd_config && \
	sed -i '/#AddressFamily any/s/^#//'  /etc/ssh/sshd_config && \
	sed -i '/AddressFamily any/s/any/inet/'  /etc/ssh/sshd_config && \
	sed -i '/PasswordAuthentication yes/s/yes/no/g' /etc/ssh/sshd_config && \
	sed -i '/#PermitRootLogin yes/s/yes/prohibit-password/' /etc/ssh/sshd_config && \
	sed -i '/#PermitRootLogin/s/^#//' /etc/ssh/sshd_config && \
	sed -i '/NAutoVTs/s/#NAutoVTs=6/NAutoVTs=0/' /etc/systemd/logind.conf && \
	sed -i '/ReserveVT/s/#ReserveVT=6/ReserveVT=0/' /etc/systemd/logind.conf && \
	echo "Ciphers chacha20-poly1305@openssh.com" >> /etc/ssh/sshd_config && \
	echo "KexAlgorithms curve25519-sha256@libssh.org" >> /etc/ssh/sshd_config && \
	echo "MACs hmac-sha2-512-etm@openssh.com" >> /etc/ssh/sshd_config && \
	echo "_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=lcd -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel -Dswing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'" >> /etc/environment && \
	systemctl enable sshd rsyslog && \
	systemctl disable auditd network

COPY home /root

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
