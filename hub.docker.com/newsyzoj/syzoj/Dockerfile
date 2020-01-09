FROM ubuntu:18.04
ENV container docker
RUN cp /etc/apt/sources.list /sources.list && apt update && apt full-upgrade -y && \
apt install python-pip python3-pip libboost-filesystem-dev build-essential p7zip-full rabbitmq-server openssh-server openssh-client git vim nano wget curl dos2unix net-tools locales apt-utils nginx clang-format software-properties-common $(check-language-support) -y && \
pip install Pygments && \
curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt install nodejs -y && \
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && apt update && apt install yarn -y && \
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8 && add-apt-repository 'deb [arch=amd64,arm64,ppc64el] http://mariadb.nethub.com.hk/repo/10.3/ubuntu bionic main' && add-apt-repository ppa:chris-lea/redis-server && \
echo "mariadb-server mysql-server/root_password password mysql" | debconf-set-selections && echo "mariadb-server mysql-server/root_password_again password mysql" | debconf-set-selections && \
apt install mariadb-server mariadb-client redis-server -y && \
apt purge software-properties-common -y && apt autoremove -y && \
rm -rf /etc/ssh/*key* /var/lib/apt/* /var/lib/rabbitmq/* /tmp/* && \
adduser --disabled-password --gecos "" syzoj && \
cd /etc/systemd/system && curl -sL -o service.tar https://newsyzoj.github.io/syzoj-docker/service.tar && tar -xf service.tar && rm service.tar && \
curl -sL -o /bin/genpass https://newsyzoj.github.io/syzoj-docker/genpass && chmod +x /bin/genpass && \
curl -sL -o /bin/genlang https://newsyzoj.github.io/syzoj-docker/genlang && chmod +x /bin/genlang && \
systemctl mask getty@tty1.service && systemctl enable mariadb rabbitmq-server redis-server nginx genpass genlang syzoj-web syzoj-judge-daemon syzoj-judge-runner@1 && \
cd /etc/nginx/sites-enabled && rm default && curl -sL -o syzoj https://newsyzoj.github.io/syzoj-docker/syzoj && \
localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 && \
sed -i /etc/redis/redis.conf -e "s/bind 127.0.0.1 ::1/bind 127.0.0.1/" && \
sed -i /etc/mysql/my.cnf -e "s/#bind-address=0.0.0.0/bind-address=0.0.0.0/" && \
sed -i /root/.bashrc -e "s/#force_color_prompt=yes/force_color_prompt=yes/" && \
mkdir -p /opt/syzoj/sandbox && chown syzoj:syzoj /opt/syzoj
ENV LANG en_US.utf8
USER syzoj
RUN sed -i /home/syzoj/.bashrc -e "s/#force_color_prompt=yes/force_color_prompt=yes/" && \
cd /opt/syzoj && git clone https://github.com/syzoj/syzoj && mv syzoj web && \
git clone https://github.com/syzoj/judge-v3 && mv judge-v3 judge && \
cd judge && yarn && yarn run build && cd .. && cd web && yarn && cd .. && \
mkdir config && cp web/config-example.json config/web.json && \
cp judge/daemon-config-example.json config/daemon.json && \
cp judge/runner-shared-config-example.json config/runner-shared.json && \
cp judge/runner-instance-config-example.json config/runner-instance-1.json && \
touch config/install && \
mv web/uploads data && ln -s ../data web/uploads && \
mkdir sessions && ln -s ../sessions web/sessions
USER root
RUN touch /opt/syzoj/config/DATABASE_ROOT_PASSWORD && chmod 600 /opt/syzoj/config/* && \
curl -sL -o /sandbox-rootfs.tar.gz https://github.com/syzoj/sandbox-rootfs/releases/download/181202/sandbox-rootfs-181202.tar.gz && \
cd /opt/syzoj/sandbox/ && tar xf /sandbox-rootfs.tar.gz && rm /sandbox-rootfs.tar.gz && \
mv /sources.list /opt/syzoj/sandbox/rootfs/etc/apt/sources.list && \
cp /etc/resolv.conf /opt/syzoj/sandbox/rootfs/etc/resolv.conf && \
printf "/etc/resolv.conf /opt/syzoj/sandbox/rootfs/etc/resolv.conf auto bind,rw,relatime,discard,data=ordered 0 0\n">/etc/fstab && \
chroot /opt/syzoj/sandbox/rootfs /bin/bash -c "\
rm -rf /var/lib/apt && apt update && apt full-upgrade -y ; apt purge ghc\* -y ; \
apt install ghc-head vim nano curl wget dos2unix locales apt-utils openssh-server openssh-client -y ; apt autoremove -y ; \
localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 && \
sed -i /root/.bashrc -e \"s/#force_color_prompt=yes/force_color_prompt=yes/\" && \
printf \"\" >/etc/resolv.conf && rm -rf /etc/ssh/*key* /var/lib/apt* /tmp/*"
STOPSIGNAL SIGRTMIN+4
CMD ["/bin/systemd"]