FROM archlinux/base:latest

RUN ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime && \
	echo 'Server = https://mirror.umd.edu/archlinux/$repo/os/$arch' >> /etc/pacman.d/mirrorlist && \
	sed -i '/#Color/s/^#//' /etc/pacman.conf && \
	sed -i '/#VerbosePkgLists/s/^#//' /etc/pacman.conf && \
	sed -i "/\[multilib\]/,/Include/"'s/^#//' /etc/pacman.conf

RUN pacman -Syyu --needed --noconfirm --quiet \
	neovim zsh zsh-syntax-highlighting zsh-autosuggestions zsh-completions zsh-theme-powerlevel9k git tig tree wget rsync curl openssl xclip xorg-xauth ncdu lsof mlocate \
	ack ccze \
	atop htop dstat iotop glances \
	tmux screen multitail \
	logrotate logwatch strace \
	lynis nikto \
	ngrep nload nethogs iftop hping autossh net-tools mtr iproute tcpdump traceroute inetutils bind-tools whois dhcping \
	elinks jq \
	unzip unrar p7zip \
	sl cowsay \
	dhcpcd iptables \
	systemd-sysvcompat base-devel multilib-devel \
	pkgfile diff-so-fancy \
	vim-airline vim-airline-themes vim-fugitive vim-nerdcommenter vim-nerdtree && \
	pacman -Scc --noconfirm

RUN sed -i -e "s/# fr_FR.UTF-8.*/fr_FR.UTF-8 UTF-8/" /etc/locale.gen && \
	echo 'fr_FR.UTF-8 UTF-8' > /etc/locale.gen && \
	locale-gen && \
	echo 'LANG=fr_FR.UTF-8' > /etc/locale.conf && \
	chsh -s /usr/bin/zsh

RUN sed -i '/ssh_host_ed25519_key/s/^#//' /etc/ssh/sshd_config && \
	sed -i '/#AddressFamily any/s/^#//'  /etc/ssh/sshd_config && \
	sed -i '/AddressFamily any/s/any/inet/'  /etc/ssh/sshd_config && \
	sed -i '/#PasswordAuthentication yes/s/^#//'  /etc/ssh/sshd_config && \
	sed -i '/PasswordAuthentication/s/yes/no/' /etc/ssh/sshd_config && \
	sed -i '/#PermitRootLogin yes/s/yes/prohibit-password/' /etc/ssh/sshd_config && \
	sed -i '/#PermitRootLogin/s/^#//' /etc/ssh/sshd_config && \
	sed -i '/#X11Forwarding no/s/no/yes/' /etc/ssh/sshd_config && \
	sed -i '/#X11Forwarding/s/^#//'  /etc/ssh/sshd_config && \
	sed -i '/NAutoVTs/s/#NAutoVTs=6/NAutoVTs=0/' /etc/systemd/logind.conf && \
	sed -i '/ReserveVT/s/#ReserveVT=6/ReserveVT=0/' /etc/systemd/logind.conf && \
	echo "Ciphers chacha20-poly1305@openssh.com" >> /etc/ssh/sshd_config && \
	echo "KexAlgorithms curve25519-sha256@libssh.org" >> /etc/ssh/sshd_config && \
	echo "MACs hmac-sha2-512-etm@openssh.com" >> /etc/ssh/sshd_config && \
	echo "_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=lcd -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel -Dswing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'" >> /etc/environment && \
	rm /etc/motd && \
	sed -i '/#Color/s/^#//' /etc/pacman.conf && \
	sed -i '/#VerbosePkgLists/s/^#//' /etc/pacman.conf && \
	pkgfile -u && \
	systemctl enable sshd && \
	echo 'Server = https://mir.archlinux.fr/$repo/os/$arch' > /etc/pacman.d/mirrorlist

COPY home /root

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]
