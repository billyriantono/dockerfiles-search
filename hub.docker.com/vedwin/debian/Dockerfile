FROM debian:stretch-slim

# ADD . /host
WORKDIR /root

ENV TERM=xterm-256color
ENV DEBIAN_FRONTEND=noninteractive
    # RUN  apt-get -y update && apt-get -y install git net-tools cmake build-essential zsh curl wget ansible vim-nox cron gnutls-bin liblockfile1 rsync man
RUN for i in {1..8}; do mkdir -p "/usr/share/man/man$i"; done  # hack to fix stretch bug https://github.com/debuerreotype/debuerreotype/issues/10
RUN apt-get -y update && apt-get -y install ansible git rsync vim-nox 
# java debian boiler plate
RUN mkdir -p /usr/share/man/man1 && \
    (echo "deb http://http.debian.net/debian jessie-backports main" > /etc/apt/sources.list.d/backports.list) && \
    apt-get update -y && \
    apt-get install -yq --no-install-recommends default-jdk

RUN apt-get install unzip -y && \
    apt-get autoremove -y
RUN git clone https://github.com/vxe/home.git && rsync -avz --exclude '.git' /root/home/ /root
WORKDIR /root/boot
RUN ansible-playbook -l localhost /root/boot/home.yml --verbose
#################################################################################
    # image specific steps
#################################################################################
# RUN ansible-playbook -l localhost /root/etc/ansible/tasks/stretch-stable.yml --verbose
    # # emacs
# RUN wget http://emacs.ganneff.de/pool/main/e/emacs-snapshot/emacs-snapshot-common_20180608+emacs-26.1-2137-gf09e9d292f-~egd9+1_all.deb
# RUN wget http://emacs.ganneff.de/pool/main/e/emacs-snapshot/emacs-snapshot-bin-common_20180608+emacs-26.1-2137-gf09e9d292f-~egd9+1_amd64.deb
# RUN wget http://emacs.ganneff.de/pool/main/e/emacs-snapshot/emacs-snapshot-nox_20180608+emacs-26.1-2137-gf09e9d292f-~egd9+1_amd64.deb
# RUN dpkg -i emacs-snapshot-common_20180608+emacs-26.1-2137-gf09e9d292f-~egd9+1_all.deb 
# RUN dpkg -i emacs-snapshot-bin-common_20180608+emacs-26.1-2137-gf09e9d292f-~egd9+1_amd64.deb
# RUN dpkg -i emacs-snapshot-nox_20180608+emacs-26.1-2137-gf09e9d292f-~egd9+1_amd64.deb

RUN curl -s "https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein" > /usr/bin/lein && chmod a+x /usr/bin/lein
RUN cd /root/server && lein clean && lein deps && lein compile

# RUN ansible-playbook -l localhost /root/etc/ansible/perl-locallib.yml --verbose
# RUN ansible-playbook -l localhost /root/etc/ansible/virtualenvs.yml --verbose
# RUN ansible-playbook -l localhost /root/etc/ansible/ruby-gems.yml --verbose
# RUN ansible-playbook -l localhost /root/etc/ansible/slow-lang.yml --verbose
#     # RUN rm -rf /root/.emacs.d/ && rsync --exclude .git --exclude var --exclude elpa -avz /host/ /root  && emacs -nw --batch -l ~/.emacs.d/init.el --eval="(+ 2 3)"
# # RUN git clone https://github.com/vxe/home.git && rsync -avz --exclude '.git' /root/home/ /root
# RUN emacs -nw --batch -l ~/.emacs.d/init.el --eval="(+ 2 3)" 


EXPOSE 5432/tcp 
EXPOSE 7199/tcp
EXPOSE 2480/tcp 
EXPOSE 8888/tcp
EXPOSE 6969/tcp
EXPOSE 3449/tcp 




