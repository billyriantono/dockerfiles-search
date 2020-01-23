FROM        debian:stretch
RUN         export TERM=xterm                                                                                               &&      \
            export DEBIAN_FRONTEND=noninteractive                                                                           &&      \
            echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections                                  &&      \
            echo "deb http://deb.debian.org/debian stretch main contrib non-free" > /etc/apt/sources.list                   &&      \
            echo "deb http://deb.debian.org/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list          &&      \
            echo "deb http://security.debian.org stretch/updates main contrib non-free" >> /etc/apt/sources.list            &&      \
            echo "deb-src http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list       &&      \
            echo "deb http://ftp.debian.org/debian/ stretch-updates main contrib non-free" >> /etc/apt/sources.list         &&      \
            echo "deb-src http://ftp.debian.org/debian/ stretch-updates main contrib non-free" >> /etc/apt/sources.list     &&      \
            dpkg --add-architecture i386                                                                                    &&      \
            apt-get update                                                                                                  &&      \
            apt-get -y install apt-utils python3                                                                            &&      \
            apt-get -y install man-db manpages                                                                              &&      \
            apt-get -y install xterm xfonts-cyrillic apt-listchanges                                                        &&      \
            apt-get -y install ncurses-term dialog ca-certificates                                                          &&      \
            apt-get -y install locales wget rsync netcat                                                                    &&      \
            rm /etc/default/locale && \
            rm /etc/locale.gen && \
            rm /etc/locale.alias
ADD         locale /etc/default/
ADD         locale.gen /etc/
ADD         locale.alias /etc/
RUN         locale-gen                                                                                                      &&      \
            export LANG=en_US.UTF8                                                                                          &&      \
            apt-get -y upgrade                                                                                              &&      \
            apt-get -y install openssl bzip2 xz-utils unzip unrar nano \
            initscripts  bash-completion && \
            apt-get -y install lsb-base lsb-release linux-base iso-codes \
            iptables gzip gnupg gnupg2 && \
            rm -rf  /var/lib/apt/lists/*
ENV			DEBIAN_FRONTEND=noninteractive
ENV			TERM=xterm
