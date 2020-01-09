FROM centos:latest

RUN set -x && \
    rm -f /etc/rpm/macros.image-language-conf && \
    sed -i '/^override_install_langs=/d' /etc/yum.conf && \
    yum -y reinstall glibc-common && \
    yum clean all && \
    yum update -y && \
    yum install -y epel-release git && \
    yum -y install ansible && \
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_asciiquarium.git /asciiquarium &&\
    cd /asciiquarium && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_cmatrix.git /cmatrix &&\
    cd /cmatrix && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_cureutils.git /cureutils &&\
    cd /cureutils && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_fortune.git /fortune &&\
    cd /fortune && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_nyancat.git /nyancat &&\
    cd /nyancat && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_beer-mug.git /beer-mug &&\
    cd /beer-mug && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_cowsay.git /cowsay &&\
    cd /cowsay && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_pong-command.git /pong-command &&\
    cd /pong-command && ansible-playbook -i localhost install.yml &&\
    git clone https://github.com/TomonoriMatsumura/ansible_joke-programs_sl.git /sl &&\
    cd /sl && ansible-playbook -i localhost install.yml

ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"
