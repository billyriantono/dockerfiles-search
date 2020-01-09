FROM alpine:latest

RUN apk update && \
	apk upgrade && \
	apk add \
	neovim zsh-vcs zsh-syntax-highlighting zsh-autosuggestions git tig tree wget rsync curl openssl xclip xauth ncdu lsof mlocate \
	ack pdsh \
	atop htop iotop glances \
	tmux screen multitail byobu \
	logrotate strace \
	nikto \
	ngrep nload nethogs iftop autossh net-tools mtr iproute2 tcpdump tcptraceroute bind-tools whois dhcping \
	elinks jq \
	unzip unrar p7zip \
	sl \
	dhcpcd iptables rsyslog \
	s6-linux-utils s6-linux-init tzdata shadow && \
	ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime && \
	ln -sf /bin/zsh /usr/bin/zsh && \
	chsh -s /bin/zsh

COPY home /root

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]
